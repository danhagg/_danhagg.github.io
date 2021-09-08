---
title: Program Execution
parent: Windows Artifacts
has_children: true
nav_order: 2
---

# Program Execution


## Amcache.hve
_C:\Windows\AppCompat\Programs\Amcache.hve_

KEYS: _Amcache.hve\RootFile\VolumeGUID\######_
- Program updater: A task associated with the Application Experience Service
- Uses the registry Amcache.hve to store data during process creation
- Keys: Programs and files
- Entries for every executable run:
- Full path info
- $Standardinfo
- Last Modification Time
- Disk Volume executable run from
- Amcaheparser.py (all) vs AmchacheParser.exe (executables with no program installer)

## BAM/DAM
_SYSTEM\CurrentControlSet\Service\bam\UserSettings\<SID>_
- Windows Background Activity Moderator
- Provides full path of the executable file that was run on the system and its last execution date/time

## Jump lists
_C:\Users\<profile>\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations_
- Object Linking Embedding Compound (OLE) Compound File (CF)
- Multiple data streams (LNKS) into a single file
- Task bar == Jump list
- Allows users to access frequently used items quickly and easily
- The data stored in AutomaticDestinations folder will each have a unique file prepended with the AppID of the associated application
- First time of execution of application.
    - Creation Time = First time item added to the AppID file.
- Last time of execution of application w/file open.
    - Modification Time = Last time item added to the AppID file.
- List of Jump List IDs ->

## Last-Visited MRU
_NTUSER.dat\Software\Windows\Microsoft\CurrentVersion\Explorer\ComDlg\LastVisitedPidMRU_
- Tracks the executable used by an application to open the files documented in the OpenSaveMRU key.
- Each value also tracks the directory location for the last file that was accessed by that application.
- notpad.exe was last run using the C:\Users\<profile>\Desktop folder

## Prefetch
_C:\Windows\Prefetch_
- Boot (no forensic value) vs application prefetching
- Default: Prefetch service tracks both types of operations
- EnablePrefetcher value (SYSTEM HIVE) of PrefetchParameters key, can be modified to track one, both, none.
- When app launched for first time a prefetch file made in the prefetch directory
- Speeds up app launch times by preloading code pages of commonly used applications.
- Cache manager monitors all files & directories referenced for each application/process & maps into a .pf file
- Not enabled by default on Windows server
- `PECmd.exe -f Windows\Prefetch\POWERPNT.EXE-A3B023EE.pf`

## Recent Apps
_NTUSER.dat\Software\Microsoft\Windows\CurrentVersion\Search\RecentApps_
- GUI Program execution launched on Windows 10 system is tracked in RecentApps key
- Each GUID is a recent application
- AppID: Name of app
- Last Access Time
- Launch Count

## Shimcache
_NSYSTEM\CurrentControlSet\Control\SessionManager\App_
- Windows Application Compatibility Database: identify application compatibility challenges with executables
- Any executable run on this system can be found with this key e.g., Malware
- Last 1,024 entries stored

## System Resource Usage Monitor (SRUM)
_C:\Windows\System32\SRU_
_SOFTWARE\Microsoft\WindowsNT\CurrentVersion\SRUM\Extensions\{GUID}_

- Records 30-60 days of historical system performance
- Applications run
- User account responsible
- Bytes sent/received per hour
- e.g., a user may have a lot of nc.exe bytes transferred

## UserAssist
_NTUSER.dat>Software\Microsoft\Windows\CurrentVersion\Explorer\ UserAssist\GUID\count_
- GUI based programs launched from Desktop are tracked in launcher on Windows 10 Count subkey: Values track shortcut information and applications launched by User
- Count subkey: Stored obfuscated by ROT13 (Right on Table) Chrome > Puebzr
- Can see the decode in User assist artifacts

## Windows 10 Timeline
_C:\Users\<profile>\AppData\Local\ConnectedDevicesPlatform\L.<profile>\ActivitiesCache.db_
- Windows 10 records recently used applications and files in a timeline accessible via “WIN + TAB”
- Data is recorded in SQLite database
