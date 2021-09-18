---
title: Collections
parent: Velociraptor
grand_parent: Tools
nav_order: 2
---

# Collections

1. Kape Triage
2. Event Logs
3. All running processes DLLs
4. Memory dumps
5. Perimeter logs
6. Offline Collector

Want to collect all servers as possible and any Desktops known to be involved in breach.


### Collections

#### 1. Kape Triage

In *velociraptor* collect kape *_BasicCollection*

Basic Collection (by Phill Moore):

`$Boot, $J, $J, $LogFile, $MFT, $Max, $Max, $SDS, $SDS, $T, $T, Amcache, Amcache, Amcache transaction files, Amcache transaction files, Desktop LNK Files, Desktop LNK Files XP, Event logs Win7+, Event logs Win7+, Event logs XP, LNK Files from C:rogramData, LNK Files from Microsoft Office Recent, LNK Files from Recent, LNK Files from Recent (XP), Local Service registry hive, Local Service registry hive, Local Service registry transaction files, Local Service registry transaction files, NTUSER.DAT DEFAULT registry hive, NTUSER.DAT DEFAULT registry hive, NTUSER.DAT DEFAULT transaction files, NTUSER.DAT DEFAULT transaction files, NTUSER.DAT registry hive, NTUSER.DAT registry hive XP, NTUSER.DAT registry transaction files, Network Service registry hive, Network Service registry hive, Network Service registry transaction files, Network Service registry transaction files, PowerShell Console Log, Prefetch, Prefetch, RECYCLER - WinXP, RecentFileCache, RecentFileCache, Recycle Bin - Windows Vista+, RegBack registry transaction files, RegBack registry transaction files, Restore point LNK Files XP, SAM registry hive, SAM registry hive, SAM registry hive (RegBack), SAM registry hive (RegBack), SAM registry transaction files, SAM registry transaction files, SECURITY registry hive, SECURITY registry hive, SECURITY registry hive (RegBack), SECURITY registry hive (RegBack), SECURITY registry transaction files, SECURITY registry transaction files, SOFTWARE registry hive, SOFTWARE registry hive, SOFTWARE registry hive, SOFTWARE registry hive, SOFTWARE registry hive (RegBack), SOFTWARE registry hive (RegBack), SOFTWARE registry transaction files, SOFTWARE registry transaction files, SOFTWARE registry transaction files, SOFTWARE registry transaction files, SRUM, SRUM, SYSTEM registry hive, SYSTEM registry hive, SYSTEM registry hive (RegBack), SYSTEM registry hive (RegBack), SYSTEM registry hive (RegBack), SYSTEM registry hive (RegBack), SYSTEM registry transaction files, SYSTEM registry transaction files, Setupapi.log Win7+, Setupapi.log Win7+, Setupapi.log XP, Syscache, Syscache transaction files, System Profile registry hive, System Profile registry hive, System Profile registry transaction files, System Profile registry transaction files, System Restore Points Registry Hives (XP), Thumbcache DB, UsrClass.dat registry hive, UsrClass.dat registry transaction files, WindowsIndexSearch, XML, XML, at .job, at .job, at SchedLgU.txt, at SchedLgU.txt`

Yields a ZIP 100,000 KB for my Desktop

Select in Config params

The triage zip file can then be downloaded from browser

#### 2. Event Logs

#### 3. All running processes, DLLs

#### 4. Memory dumps

#### 5. Perimeter logs (We can apparently embed exe in velo)

- VPN logs
- Firewall logs
- How did Thomas collect these?

#### 6. Offline Collector

[Offline Triage](https://docs.velociraptor.app/docs/offline_triage/)

Include third party binaries
Sometimes we want to collect the output from other third party executables. It would be nice to be able to package them together with *velociraptor* and include their output in the collection file.

Velociraptor fully supports incorporating external tools. When creating the offline collection, *velociraptor* will automatically pack any third party binaries it needs to collect the artifacts specified.

### Upload files to *ShareFile*
