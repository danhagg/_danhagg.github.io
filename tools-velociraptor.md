---
title: Velociraptor
parent: Tools
has_children: true
nav_order: 3
---

# Velociraptor

## 1. Velociraptor Deployments
    1. Create config files
    2. Deploy exe and config files to network
    3. GPO's?


## 2. Collections




### 1. Velociraptor Deployments

Generate config files
```PowerShell
velociraptor config generate -i
```

- ScreenConect into clients network
- Delpoy velociraptor (as executable)
- Can make the config files in advance
    - server config file (for Windows)
    - client config file (for Windows)
- Run files as administrator 

```PowerShell
velociraptor --config server.config.yaml frontend -v
velociraptor --config client.config.yaml client -v

```

In velociraptor collect kape Basic collection

Basic Collection (by Phill Moore): 

$Boot, $J, $J, $LogFile, $MFT, $Max, $Max, $SDS, $SDS, $T, $T, Amcache, Amcache, Amcache transaction files, Amcache transaction files, Desktop LNK Files, Desktop LNK Files XP, Event logs Win7+, Event logs Win7+, Event logs XP, LNK Files from C:rogramData, LNK Files from Microsoft Office Recent, LNK Files from Recent, LNK Files from Recent (XP), Local Service registry hive, Local Service registry hive, Local Service registry transaction files, Local Service registry transaction files, NTUSER.DAT DEFAULT registry hive, NTUSER.DAT DEFAULT registry hive, NTUSER.DAT DEFAULT transaction files, NTUSER.DAT DEFAULT transaction files, NTUSER.DAT registry hive, NTUSER.DAT registry hive XP, NTUSER.DAT registry transaction files, Network Service registry hive, Network Service registry hive, Network Service registry transaction files, Network Service registry transaction files, PowerShell Console Log, Prefetch, Prefetch, RECYCLER - WinXP, RecentFileCache, RecentFileCache, Recycle Bin - Windows Vista+, RegBack registry transaction files, RegBack registry transaction files, Restore point LNK Files XP, SAM registry hive, SAM registry hive, SAM registry hive (RegBack), SAM registry hive (RegBack), SAM registry transaction files, SAM registry transaction files, SECURITY registry hive, SECURITY registry hive, SECURITY registry hive (RegBack), SECURITY registry hive (RegBack), SECURITY registry transaction files, SECURITY registry transaction files, SOFTWARE registry hive, SOFTWARE registry hive, SOFTWARE registry hive, SOFTWARE registry hive, SOFTWARE registry hive (RegBack), SOFTWARE registry hive (RegBack), SOFTWARE registry transaction files, SOFTWARE registry transaction files, SOFTWARE registry transaction files, SOFTWARE registry transaction files, SRUM, SRUM, SYSTEM registry hive, SYSTEM registry hive, SYSTEM registry hive (RegBack), SYSTEM registry hive (RegBack), SYSTEM registry hive (RegBack), SYSTEM registry hive (RegBack), SYSTEM registry transaction files, SYSTEM registry transaction files, Setupapi.log Win7+, Setupapi.log Win7+, Setupapi.log XP, Syscache, Syscache transaction files, System Profile registry hive, System Profile registry hive, System Profile registry transaction files, System Profile registry transaction files, System Restore Points Registry Hives (XP), Thumbcache DB, UsrClass.dat registry hive, UsrClass.dat registry transaction files, WindowsIndexSearch, XML, XML, at .job, at .job, at SchedLgU.txt, at SchedLgU.txt

Yields a ZIP 100,000 KB for my Desktop

Select in Config params

Too long path
`C:\Users\dhaggerty\OneDrive - The Pronet Group\Velociraptor\self_triage_config`
So make dir on `C:\v`

The triage zip file can then be downloaded from browser

Want to collect all servers as possible and any Desktops invlved in breach

All running processes DLLs

Memory dumps

Perimeter logs

## What logs can be collected 
VPN
Firewall

## GPO


## Offline Collector
https://docs.velociraptor.app/docs/offline_triage/

Include third party binaries
Sometimes we want to collect the output from other third party executables. It would be nice to be able to package them together with Velociraptor and include their output in the collection file.

Velociraptor fully supports incorporating external tools. When creating the offline collection, Velociraptor will automatically pack any third party binaries it needs to collect the artifacts specified.

