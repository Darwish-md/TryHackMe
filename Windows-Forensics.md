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

These two sources complement each other in registry forensics, with transaction logs providing real-time changes and backups offering historical snapshots.
