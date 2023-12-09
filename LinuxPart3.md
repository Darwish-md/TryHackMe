## Commands
- wget
- SCP (copy files with ssh)
  - `scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt` to copy a file important.txt from local machine to remote 192.168.1.30 and will be called transferred.txt.
  - `scp ubuntu@192.168.1.30:/home/ubuntu/documents.txt notes.txt` to copy a file called documents,txt from remote 192.168.1.30 to local machine and will be called notes.txt.
- Python `HTTPServer` turns your computer into a quick and easy web server that you can use to serve your own files, where they can then be downloaded by another computing using commands such as curl and wget.
  - `python3 -m http.server` is used to start an hhtp server in the directory where the command was run.
  - `wget http://{machineIP}:8000/{some file name}` is used to download some file from the webserver hosted on the {machineIP}.
## Notes
- 
