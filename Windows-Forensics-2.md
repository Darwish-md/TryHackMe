Computer scientists have created different file systems that organize the bits in a hard drive as per a standard, so that information stored in these bits can be interpreted easily.

### FAT (File Allocation Table)
The File Allocation Table creates a table that indexes the location of bits that are allocated to different files. It has been in place since 1970s, but is not the default anymore.

#### Data Structures of FAT
The FAT file system supports the following Data structures:
1. Clusters:
A cluster is a basic storage unit of the FAT file system. Each file stored on a storage device can be considered a group of clusters containing bits of information.
2. Directory:
A directory contains information about file identification, like file name, starting cluster, and filename length.
3. File Allocation Table:
The File Allocation Table is a linked list of all the clusters. It contains the status of the cluster and the pointer to the next cluster in the chain.

In summary, the bits that make up a file are stored in clusters. All the filenames on a file system, their starting clusters, and their lengths are stored in directories. And the location of each cluster on the disk is stored in the File Allocation Table. 

#### Variations of FAT
The FAT file format divides the available disk space into clusters for more straightforward addressing. The number of these clusters depends on the number of bits used to address the cluster. Hence the different variations of the FAT file system. 

- Theoretically, FAT12 used 12-bit cluster addressing for a maximum of 4096 clusters(2^12).
- FAT16 used 16-bit cluster addressing for a maximum of 65,536 clusters (2^16).
- FAT32, the actual bits used to address clusters are 28, so the maximum number of clusters is actually 268,435,456 or 2^28.

##### exFAT
As the file sizes have grown, especially with higher resolution images and videos being supported by the newer digital cameras, the maximum file size limit of FAT32 became a substantial limiting factor for camera manufacturers. Though Microsoft had moved on to the NTFS file system, it was not suitable for digital media devices as they did not need the added security features and the overhead that came with it. Therefore, these manufacturers lobbied Microsoft to create the exFAT file system.

- The exFAT file system is now the default for SD cards larger than 32GB, ad is widely adopted by digitial manufactureres. 
- The exFAT file system supports a cluster size of 4KB to 32MB. It has a maximum file size and a maximum volume size of 128PB (Petabytes).
- It also reduces some of the overheads of the FAT file system to make it lighter and more efficient.
- It can have a maximum of 2,796,202 files per directory.

### NTFS (New Technology File System)
it offers little more in terms of security, reliability, and recovery capabilities. It also has certain limitations when it comes to file and volume sizes. 

#### NTFS Features:
- ***Journaling***: NTFS incorporates journaling to log metadata changes, aiding system recovery from crashes or data movements. This log, stored in $LOGFILE within the volume's root directory, defines NTFS as a journaling file system.
- ***Access Controls***: NTFS implements access controls, assigning ownership and permissions for files/directories to individual users.
- ***Volume Shadow Copies***: This feature tracks file changes, enabling users to restore previous file versions for recovery or system restoration purposes. However, in recent ransomware attacks, perpetrators delete shadow copies to hinder victim data recovery.
- ***Alternate Data Streams***: ADS permit files to contain multiple data streams within a single file. While browsers like Internet Explorer utilize ADS for identifying internet-downloaded files, malware exploits this feature to conceal code within files for covert operations.

#### Master File Table
 NTFS file system data is organized in the Master File Table. From a forensics point of view, the following are some of the critical files in the MFT:
 - $MFT: the first record in the volume. The Volume Boot Record (VBR) points to the cluster where it is located. $MFT stores information about the clusters where all other objects present on the volume are located. This file contains a directory of all the files present on the volume.
 - $LOGFILE: stores the transactional logging of the file system. It helps maintain the integrity of the file system in the event of a crash.
 - $UsnJrnl: stands for the Update Sequence Number (USN) Journal. It is present in the $Extend record. It contains information about all the files that were changed in the file system and the reason for the change. It is also called the change journal.

#### MFT Explorer is one of Eric Zimmerman's tools used to explore MFT files.
