- A processor in a computer running Windows has two different modes: ***user mode*** and ***kernel mode***. The processor switches between the two modes depending on what type of code is running on the processor.
 Applications run in user mode, and core operating system components run in kernel mode. While many drivers run in kernel mode, some drivers may run in user mode.

## Processes:
### 1. `System`:
***What is unusual behaviour for this process?***
- A parent process (aside from System Idle Process (0))
- Multiple instances of System. (Should only be one instance) 
- A different PID. (Remember that the PID will always be PID 4)
- Not running in Session 0
  
### 2. `smss.exe` (session manager subsystem):
- The first user-mode process started by the kernel.
- This process starts the kernel and user modes of the Windows subsystem.
- This subsystem includes `win32k.sys` (kernel mode), `winsrv.dll` (user mode), and `csrss.exe` (user mode).
- `Smss.exe` starts `csrss.exe` (Windows subsystem) and `wininit.exe` in Session 0, an isolated Windows session for the operating system, and `csrss.exe` and `winlogon.exe` for Session 1, which is the user session.
  
***What is unusual?***
- A different parent process other than System (4)
- The image path is different from C:\Windows\System32
- More than one running process. (children self-terminate and exit after each new session)
- The running User is not the SYSTEM user
- Unexpected registry entries for Subsystem

### 3. `csrss.exe` (Client Server Runtime subsystem)
- The user-mode side of the Windows subsystem.
- This process is responsible for the Win32 console window and process thread creation and deletion as well as making the Windows API available to other processes, mapping drive letters, and handling the Windows shutdown process

***What is unusual?***
- An actual parent process. (smss.exe calls this process and self-terminates)
- Image file path other than C:\Windows\System32
- Subtle misspellings to hide rogue processes masquerading as csrss.exe in plain sight
- The user is not the SYSTEM user.

### 4. `wininit.exe`:
- The Windows Initialization Process, wininit.exe, is responsible for launching services.exe (Service Control Manager), lsass.exe (Local Security Authority), and lsaiso.exe (only if credential guard is enabled) within Session 0.

***What is unusual?***
- An actual parent process. (smss.exe calls this process and self-terminates)
- Image file path other than C:\Windows\System32
- Subtle misspellings to hide rogue processes in plain sight
- Multiple running instances
- Not running as SYSTEM

### 5. `services.exe` Service Control Manager (SCM):
- Its primary responsibility is to handle system services: ***loading services, interacting with services and starting or ending services***. It maintains a database that can be queried using a Windows built-in utility, `sc.exe`
- Information regarding services is stored in the registry, ```HKLM\System\CurrentControlSet\Services```
