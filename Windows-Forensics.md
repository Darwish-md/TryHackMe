### Forensic artifacts
Forensic artifacts are essential pieces of information that provide evidence of human activity. For example, during the investigation of a crime scene, fingerprints, a broken button of a shirt or coat, the tools used to perform the crime are all considered forensic artifacts. All of these artifacts are combined to recreate the story of how the crime was committed. 

### Windows Registry
The Windows Registry is a collection of databases that contains the system's configuration data. This configuration data can be about the hardware, the software, or the user's information.

- The Windows registry consists of Keys and Values. When you open the `regedit.exe` utility to view the registry, the folders you see are Registry Keys. Registry Values are the data stored in these Registry Keys.
- A `Registry Hive` is a group of Keys, subkeys, and values stored in a single file on the disk.
- The registry on any Windows system contains the following five root keys:
  - HKEY_CURRENT_USER
  - HKEY_USERS
  - HKEY_LOCAL_MACHINE
  - HKEY_CLASSES_ROOT (The `HKEY_LOCAL_MACHINE\Software\Classes` key contains default settings that can apply to all users on the local computer. The `HKEY_CURRENT_USER\Software\Classes` key has settings that override the default settings and apply only to the interactive user. The `HKEY_CLASSES_ROOT` key provides a view of the registry that merges the information from these two sources.)
  - HKEY_CURRENT_CONFIG

### Accessing Registry Hives offline
if we only have access to a disk image and we cannot use regedit.exe, then we need to know where these hives are located. 

1- The majority are located in `C:\Windows\System32\Config` directory and are:
  1. DEFAULT (mounted on HKEY_USERS\DEFAULT)
  2. SAM (mounted on HKEY_LOCAL_MACHINE\SAM)
  3. SECURITY (mounted on HKEY_LOCAL_MACHINE\Security)
  4. SOFTWARE (mounted on HKEY_LOCAL_MACHINE\Software)
  5. SYSTEM (mounted on HKEY_LOCAL_MACHINE\System)

2- Two other hives containing user information can be found in the User profile directory `C:\Users\<USERNAME>`:
  1. `NTUSER.DAT` (mounted on HKEY_CURRENT_USER when a user logs in) => located in `C:\Users\<username>\`
  2. `USRCLASS.DAT` (mounted on HKEY_CURRENT_USER\Software\CLASSES) => located in `C:\Users\<username>\AppData\Local\Microsoft\Windows`

3- There is another very important hive called the AmCache hive located in `C:\Windows\AppCompat\Programs\Amcache.hve`. Windows creates this hive to save information on programs that were recently run on the system.

4- Transaction logs and Backups: 

=> Registry Transaction Logs:
- Serve as journals of changes made to registry hives.
- Windows frequently uses transaction logs during registry writes.
- May contain the latest changes not yet written to the registry hives.
- Stored as .LOG files in the same directory as the hives. For example, the transaction log for the ***SAM hive*** will be located in `C:\Windows\System32\Config` in the filename ***SAM.LOG***.
- Multiple transaction logs may exist, indicated by extensions like .LOG1, .LOG2.

=> Registry Backups:
- Act as backups of registry hives.
- Copies of hives are stored in the `C:\Windows\System32\Config\RegBack` directory approximately every ten days.

  > These two sources complement each other in registry forensics, with transaction logs providing real-time changes and backups offering historical snapshots.

### Data Aquisition
For the sake of accuracy, it is recommended practice to image the system or make a copy of the required data and perform forensics on it. This process is called data acquisition. 

We can't copy the registry hives since it is restricted, and hence we use tools such as: {KAPE, Autopsy, FTK Imager}.

### Exploring the registry
Since registry editor only works with live system, and doesn't work with exported hives, we use tools like: {Registry Viewer, Zimmerman's Registry Explorer, RegRipper}.

### Now let's find out where to look in the registry to perform our forensic analysis:

#### System information and system accounts
- To find the ***OS version***, we can use the following registry key: `SOFTWARE\Microsoft\Windows NT\CurrentVersion`
- The hives containing the machine’s configuration data used for controlling system startup are called ***Control Sets***. Commonly, we will see two Control Sets, ***ControlSet001*** and ***ControlSet002***. their locations: `SYSTEM\ControlSet001` and `SYSTEM\ControlSet002`
- Windows creates a volatile Control Set when the machine is live, called the ***CurrentControlSet*** (`HKLM\SYSTEM\CurrentControlSet`).
- the last known good configuration can be found using the following registry value: `SYSTEM\Select\LastKnownGood`.
- We can find the ***Computer Name*** from the following location: `SYSTEM\CurrentControlSet\Control\ComputerName\ComputerName`.
- For finding the ***Time Zone Information***, we can look at the following location: `SYSTEM\CurrentControlSet\Control\TimeZoneInformation`.
- Network Interfaces and Past Networks can be found in the key: `SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces`.
- The past networks a given machine was connected to can be found in the following locations:
  - `SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Signatures\Unmanaged`
  - `SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Signatures\Managed`
- Autostart Programs (Autoruns) can be found in the following keys:
  - `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Run`
  - `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\RunOnce`
  - `SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce`
  - `SOFTWARE\Microsoft\Windows\CurrentVersion\policies\Explorer\Run`
  - `SOFTWARE\Microsoft\Windows\CurrentVersion\Run`
- The following registry key contains information about ***services***: `SYSTEM\CurrentControlSet\Services`.
- SAM hive and user information: `SAM\Domains\Account\Users`.
  
#### Usage/knowledge of files/folders
- Windows maintains a list of recently opened files for each user and this information is stored in the NTUSER hive and can be found on the following location: `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs`.
> Shellbags are a forensic artifact in Windows systems that store information about the browsing history and navigation patterns of users within the Windows Explorer shell. These artifacts are created and maintained by the operating system to track folder views, window positions, and other settings associated with file system interactions. these information can be found here:
   - `USRCLASS.DAT\Local Settings\Software\Microsoft\Windows\Shell\Bags`
   - `USRCLASS.DAT\Local Settings\Software\Microsoft\Windows\Shell\BagMRU`
   - `NTUSER.DAT\Software\Microsoft\Windows\Shell\BagMRU`
   - `NTUSER.DAT\Software\Microsoft\Windows\Shell\Bags`
- Open/Save and LastVisited Dialog MRUs can be found here:
  - `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSavePIDlMRU`
  - `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\LastVisitedPidlMRU`
- The paths typed in the Windows Explorer address bar or searches performed can be found using the following registry keys:
  - `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\TypedPaths`
  - `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\WordWheelQuery`
  
#### Evidence of Execution
- These keys contain information about the programs launched, the time of their launch, and the number of times they were executed: `NTUSER.DAT\Software\Microsoft\Windows\Currentversion\Explorer\UserAssist\{GUID}\Count`. Programs that were run using the command line can't be found in the User Assist keys.
- ***ShimCache*** is a mechanism used to keep track of application compatibility with the OS and tracks all applications launched on the machine: `SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache`.
- AMCache stores additional data related to program executions including execution path, installation, execution and deletion times, and SHA1 hashes of the executed programs. This hive is located in the file system at: `C:\Windows\appcompat\Programs\Amcache.hve`
- Information about the last executed programs can be found at the following location in the hive: `Amcache.hve\Root\File\{Volume GUID}\`
- BAM (Background Activity Monitor)/DAM (Desktop Activity Moderator):
  - `SYSTEM\CurrentControlSet\Services\bam\UserSettings\{SID}`
  - `SYSTEM\CurrentControlSet\Services\dam\UserSettings\{SID}`

#### USB Devices
- The following locations keep track of USB keys plugged into a system:
  - `SYSTEM\CurrentControlSet\Enum\USBSTOR`
  - `SYSTEM\CurrentControlSet\Enum\USB`
- The following registry key tracks the first time the device was connected, the last time it was connected and the last time the device was removed from the system: `SYSTEM\CurrentControlSet\Enum\USBSTOR\Ven_Prod_Version\USBSerial#\Properties\{83da6326-97a6-4088-9453-a19231573b29}\####`.
- The device name of the connected drive can be found at the following location: `SOFTWARE\Microsoft\Windows Portable Devices\Devices`.

## Summary
![image](https://github.com/Darwish-md/TryHackMe/assets/72353586/6f2338b5-db9c-4e18-962b-22d9da3f2ada)
