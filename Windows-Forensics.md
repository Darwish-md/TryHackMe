### Forensic artifacts
Forensic artifacts are essential pieces of information that provide evidence of human activity. For example, during the investigation of a crime scene, fingerprints, a broken button of a shirt or coat, the tools used to perform the crime are all considered forensic artifacts. All of these artifacts are combined to recreate the story of how the crime was committed. 

### Windows Registry
The Windows Registry is a collection of databases that contains the system's configuration data. This configuration data can be about the hardware, the software, or the user's information.

- The Windows registry consists of Keys and Values. When you open the regedit.exe utility to view the registry, the folders you see are Registry Keys. Registry Values are the data stored in these Registry Keys.
- A Registry Hive is a group of Keys, subkeys, and values stored in a single file on the disk.
- The registry on any Windows system contains the following five root keys:
  - HKEY_CURRENT_USER
  - HKEY_USERS
  - HKEY_LOCAL_MACHINE
  - HKEY_CLASSES_ROOT (The `HKEY_LOCAL_MACHINE\Software\Classes` key contains default settings that can apply to all users on the local computer. The `HKEY_CURRENT_USER\Software\Classes` key has settings that override the default settings and apply only to the interactive user. The `HKEY_CLASSES_ROOT` key provides a view of the registry that merges the information from these two sources.)
  - HKEY_CURRENT_CONFIG
