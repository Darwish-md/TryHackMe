
# Linux commands
- ls
- whoami
- cd
- cat
- pwd
- echo
- cat
- `find -name passwords.txt`
- `grep "text" file.txt`
- wc -l -b to count entries by byte or line etc

- wget
  
- SCP (copy files with ssh)
  - `scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt` to copy a file important.txt from local machine to remote 192.168.1.30 and will be called transferred.txt.
  - `scp ubuntu@192.168.1.30:/home/ubuntu/documents.txt notes.txt` to copy a file called documents,txt from remote 192.168.1.30 to local machine and will be called notes.txt.
    
- Python `HTTPServer` turns your computer into a quick and easy web server that you can use to serve your own files, where they can then be downloaded by another computing using commands such as curl and wget.
  - `python3 -m http.server` is used to start an hhtp server in the directory where the command was run.
  - `wget http://{machineIP}:8000/{some file name}` is used to download some file from the webserver hosted on the {machineIP}.
    
- `ps` command is used to provide a list of the running processes as our user's session and some additional informationo. To see the processes run by other users and those that don't run from a session (i.e. system processes), we need to provide aux to the ps command like so: `ps aux`
  
- `top` gives you real-time statistics about the processes running on your system instead of a one-time view.

- To kill a process, we can use the appropriately named `kill` command and the associated PID that we wish to kill. ex: `kill 1337`. Below are some of the signals that we can send to a process when it is killed:
  - `SIGTERM` Kill the process, but allow it to do some cleanup tasks beforehand
  - `SIGKILL` Kill the process - doesn't do any cleanup after the fact
  - `SIGSTOP` Stop/suspend a process

- `systemctl [option] [service]` is used to interact with systemd process/daemon. ex: `systemctl start apache2`.

- With our process backgrounded using either Ctrl + Z or the & operator, we can use fg to bring this back to focus

- crontabs are files with specific formatting that can be recognised by `cron` process which is used to automate processes. 6 values are needed `MIN HOUR DOM MON DOW CMD`, ex: crontab file will have the command `0 *12 * * * cp -R /home/cmnatic/Documents /var/backups/` which is used to exceute the backup every 12 hours. `crontab -e` is used to add, edit, or delete a cron job.


## Notes
- The operator & allows us to execute commands in the background.
- "&&" is used to make a list of commands to run for example command1 && command2
- ">>" is used to append, and > is used to override. ex: `echo text > file.txt`

