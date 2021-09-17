---
title: Velociraptor
parent: Tools
has_children: true
nav_order: 3
---

# Velociraptor

## *velociraptor* Deployments

1. Create config files
2. Deploy *velociraptor* and config files to network
3. SCCM or Group Policy to add the MSI to the assigned software group

## Collections

1. Kape Triage
2. Event Logs
3. All running processes DLLs
4. Memory dumps
5. Perimeter logs
6. Offline Collector

Want to collect all servers as possible and any Desktops known to be involved in breach.

### *velociraptor* Deployments

#### 1. Generate config files

Download *velociraptor* as MSI to own machine. Add `exe` to PATH.

Use interactive `-i` to generate all sorts of config files for different scenarios and OS.

```PowerShell
velociraptor config generate -i
```

The same *velociraptor* binary can be run as a server or client depending upon which config file it uses: `server` or `client`.

#### 2. Deploy velociraptor,exe and config files to network

- We can use ScreenConnect to access clients network
- Recommeded way of deploying *velociraptor* to clients [here](https://docs.velociraptor.app/docs/deployment/clients/)
  - That is we download *velociraptor* MSI and install (Client IT or ourselves)
  - The advantages are that most enterprise system administration tools are used to deploying software in MSI packages.
  - One of the main benefits in using the official *velociraptor* MSI is that the MSI and the executable are signed. Windows Defender aggressively quarantines unsigned binaries, so it is highly recommended that *velociraptor* be signed.
  - When *velociraptor* starts, it attempts to load the configuration file from `C:\Program Files\Velociraptor\Velociraptor.config.yaml`.
  - Therefore you can use SCCM or Group Policy (see below) to add the MSI to the assigned software group.
  - So to summarise, when installing from the official MSI package you need to:
    - Assign the MSI via Group Policy, or use some other method to deploy the official MSI installer.
    - Copy the configuration file from a share to the *velociraptor* program directory. This can be done via Group Policy Scheduled tasks or another way (see the Group Policy procedure outlined below). As soon as the configuration file is copied, *velociraptor* will begin communicating with the server.
- As we made the `server` and `client` config files in advance we can transfer them via ScreenConnect
- Run velocirator and config files from PowerShell as Administrator

*Note:* When I start *velociraptor* from the following directory `C:\Users\<user>\OneDrive - The Pronet Group\Velociraptor\self_triage_config` I often get a `path too long` warning for some file or other that *velociraptor* collects during triage. In order to avoid this put the `server` and `client` config files with the `velociraptor.exe` in a short-named directory such as `C:\v`.

Run *velociraptor*

```PowerShell
velociraptor --config server.config.yaml frontend -v
velociraptor --config client.config.yaml client -v
```

Visit `https://127.0.0.1:8889` to access *velociraptor* GUI. Accept the SSL warnings.

#### 3. SCCM or Group Policy to add the MSI to the assigned software group

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

### Artifacts that *velociraptor* can collect

[Windows Artifacts](https://www.velocidex.com/docs/artifacts/windows_system/)

[Server Artifacts](https://www.velocidex.com/docs/artifacts/server/)

[Linux Artifacts](https://www.velocidex.com/docs/artifacts/linux/)

[Miscellaneous Artifacts](https://www.velocidex.com/docs/artifacts/misc/)
