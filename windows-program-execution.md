---
title: Program Execution
parent: Windows Artifacts
has_children: true
nav_order: 2
---

# Program Execution

## Location

_\Windows\System32\config_ and the _\Windows.Old_ folder

## INFO: 
- Global hives: SYSTEM, SAM, SOFTWARE, SECURITY
- User hives: NTUSER.DAT and UsrClass.dat profile folder
- A hierarchical database that stores configuration information
- Each 4096 section after regf block begins with header value hbin
- hbin blocks stores keys, subkeys, values for registry file, has allocated/unallocated space (if User deleted, recovery still possible)

## OS Info
_SOFTWARE\Microsoft\Windows NT\CurrentVersion_
- Version/Build Number
- Installation date/time
- Digital Product key info
- installation path
- product name
- registration for OS

_SYSTEM\ControlSet001\Control\ComputerName_

_SYSTEM\ControlSet001\Control\Windows\ShutdownTime_
    - Value stored as 8-byte Windows date & time in hexadecimal

_SYSTEM\ControlSet001\Control\FileSystem NtfsDisableLastAccessUpdate_

## Explorer in Registry
_HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer_
- _\ComDlg3_
    - _\LastVisitedPidlMRU_		Binaries used to open
    - _\OpenSavePidlMRU_		Filepaths
- _\RecentDocs_				    Recent things open/saved
- _\RunMRU_				        Last items from run box
- _\TypedPaths_				    Explicitly typed paths (even deleted)
- _\UserAssist_				    Executed programs (List of GUIDs, # of executions/times
