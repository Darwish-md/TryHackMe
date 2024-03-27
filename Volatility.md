### What is Volatility?
Volatility is a tool used in memory forensics to analyze memory dumps of different OS to identify the traces of malwares.

### Extracting memory dumps
- Listed below are a few of the techniques and tools that can be used to extract a memory from a bare-metal machine:
  - FTK Imager
  - Redline
  - DumpIt.exe
  - win32dd.exe / win64dd.exe
  - Memoryze
  - FastDump
    
  > Most of the tools mentioned above for memory extraction will output a .raw file with some exceptions like Redline that can use its own agent and session structure.

- For virtual machines, gathering a memory file can easily be done by collecting the virtual memory file from the host machine’s drive. This file can change depending on the hypervisor used; listed below are a few of the hypervisor virtual memory files you may encounter:
  - VMWare - .vmem
  - Hyper-V - .bin
  - Parallels - .mem
  - VirtualBox - .sav file *this is only a partial memory file

### Identifying image info and profiles
- With Volatility3, we don't need to worry about identifying the OS profile of the system where the memory file was dumped. We can simply use the plugin ***imageinfo*** like `python3 vol.py -f <file> imageinfo`.
- If we are still looking to get information about what the host is running from the memory dump, we can use the following three plugins `windows.info` `linux.info` `mac.info`. This plugin will provide information about the host from the memory dump: `python3 vol.py -f <file> windows.info`.

### Listing processes and connections
- `python3 vol.py -f <file> windows.pslist` is used to list all processes in the file. however some malwares, typically rootkits, can unlink itself from the list to hide. To combat this evasion technique, we can use `psscan` instead.
- The third process plugin `pstree` will list all processes based on their parent process ID, using the same methods as pslist. This can be useful for an analyst to get a full story of the processes and what may have been occurring at the time of extraction.
- `netstat` will attempt to identify all memory structures with a network connection. However, this is sometimes unstable and you can utilize other tools like ***bulk_extractor*** to extract a PCAP file from the memory file.
- `dlllist` will list all DLLs associated with processes at the time of extraction. This can be especially useful once you have done further analysis and can filter output to a specific DLL that might be an indicator for a specific type of malware you believe to be present on the system.

### Hunting & Detection capabilities
- `malfind` will attempt to identify injected processes and their PIDs along with the offset address and a Hex, Ascii, and Disassembly view of the infected area. The plugin works by scanning the heap and identifying processes that have the executable bit set RWE or RX and/or no memory-mapped file on disk (file-less malware).
- `yarascan` plugin will search for strings, patterns, and compound rules against a rule set.

### Advanced Memory Forensics
- When dealing with an advanced adversary, you may encounter malware, most of the time rootkits that will employ very nasty evasion measures that will require you as an analyst to dive into the drivers, mutexes, and hooked functions.
- hooking and driver manipulation are two types of evasion techniques. </br>
  > Hooking involves intercepting and altering function calls in software. It's used in both legitimate and malicious contexts. It works by intercepting calls before they reach their intended destination, then altering parameters or redirecting the call. There are five methods of hooking used by adversaies: {SSDT Hooks, IRP Hooks, IAT Hooks, EAT Hooks, Inline Hooks}
#### EXs of plugins provided by Volatility for such cases
- `ssdt` plugin will search for hooking and output its results. </br>
  > SSDT stands for System Service Descriptor Table; the Windows kernel uses this table to look up system functions. An adversary can hook into this table and modify pointers to point to a location the rootkit controls.
- `modules` plugin will dump a list of loaded kernel modules; this can be useful in identifying active malware. However, if a malicious file is idly waiting or hidden, this plugin may miss it.
- `driverscan` plugin will scan for drivers present on the system at the time of extraction. This plugin can help to identify driver files in the kernel that the modules plugin might have missed or were hidden.
- `handles` plugin can be used to get the resources that a process has open, such as files, registry keys, or network connections. we can use it with `| grep <process_id>`.
- `filescan` plugin can be used to identify all files loaded from the malware working directory.
### Notes:
- To get info about a specific process: `vol.py -f <dump> -o /dir/to/store_dump/ windows.memmap.Memmap --pid <suspicious PID> --dump`, then we can analyze the dmp file with `strings`.
