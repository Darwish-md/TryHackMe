- A processor in a computer running Windows has two different modes: ***user mode*** and ***kernel mode***. The processor switches between the two modes depending on what type of code is running on the processor.
 Applications run in user mode, and core operating system components run in kernel mode. While many drivers run in kernel mode, some drivers may run in user mode.

## Processes:
### 1. `System`:
What is unusual behaviour for this process?
- A parent process (aside from System Idle Process (0))
- Multiple instances of System. (Should only be one instance) 
- A different PID. (Remember that the PID will always be PID 4)
- Not running in Session 0
  
### 2. `smss.exe` (session manager subsystem):

