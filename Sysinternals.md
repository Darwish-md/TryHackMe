- The Sysinternals tools is a compilation of over 70+ Windows-based tools.

### Add to system variables to run from cmd:
- The System Properties can be launched via the command line by running `sysdm.cpl`. Click on the Advanced tab.
- Add the path to the `System variables`.

### Run sysinternals:
- To run sysinternals, we can downaload and install the suite\specific tool, or we can run it from live.sysinternals.com.
#### prerequistes to run the live version:
1. Network Discovery needs to be enabled:
   - Use command `control.exe /name Microsoft.NetworkAndSharingCenter`.
   - Click on Change advanced sharing settings and select Turn on network discovery for your current network profile.
2. Install WebDAV Redirector: `Install-WindowsFeature WebDAV-Redirector –Restart` and verify using `Get-WindowsFeature WebDAV-Redirector | Format-Table –Autosize`
3. The WebDAV client must be installed and running on the machine. The WebDAV protocol is what allows a local machine to access a remote machine running a WebDAV share and perform actions in it.
   - On a Windows 10 client, the WebDAV client is installed but the client is most likely not running. to verify the status: `get-service webclient` and to start it `start-service webclient`.
4. run a tool like `\\live.sysinternals.com\tools\procmon`.
