## Commands
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
## Notes
- 
