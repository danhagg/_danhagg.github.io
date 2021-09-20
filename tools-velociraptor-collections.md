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

```Markdown
$Boot, $J, $J, $LogFile, $MFT, $Max, $Max, $SDS, $SDS, $T, $T, Amcache, Amcache, Amcache transaction files, Amcache transaction files, Desktop LNK Files, Desktop LNK Files XP, Event logs Win7+, Event logs Win7+, Event logs XP, LNK Files from C:rogramData, LNK Files from Microsoft Office Recent, LNK Files from Recent, LNK Files from Recent (XP), Local Service registry hive, Local Service registry hive, Local Service registry transaction files, Local Service registry transaction files, NTUSER.DAT DEFAULT registry hive, NTUSER.DAT DEFAULT registry hive, NTUSER.DAT DEFAULT transaction files, NTUSER.DAT DEFAULT transaction files, NTUSER.DAT registry hive, NTUSER.DAT registry hive XP, NTUSER.DAT registry transaction files, Network Service registry hive, Network Service registry hive, Network Service registry transaction files, Network Service registry transaction files, PowerShell Console Log, Prefetch, Prefetch, RECYCLER - WinXP, RecentFileCache, RecentFileCache, Recycle Bin - Windows Vista+, RegBack registry transaction files, RegBack registry transaction files, Restore point LNK Files XP, SAM registry hive, SAM registry hive, SAM registry hive (RegBack), SAM registry hive (RegBack), SAM registry transaction files, SAM registry transaction files, SECURITY registry hive, SECURITY registry hive, SECURITY registry hive (RegBack), SECURITY registry hive (RegBack), SECURITY registry transaction files, SECURITY registry transaction files, SOFTWARE registry hive, SOFTWARE registry hive, SOFTWARE registry hive, SOFTWARE registry hive, SOFTWARE registry hive (RegBack), SOFTWARE registry hive (RegBack), SOFTWARE registry transaction files, SOFTWARE registry transaction files, SOFTWARE registry transaction files, SOFTWARE registry transaction files, SRUM, SRUM, SYSTEM registry hive, SYSTEM registry hive, SYSTEM registry hive (RegBack), SYSTEM registry hive (RegBack), SYSTEM registry hive (RegBack), SYSTEM registry hive (RegBack), SYSTEM registry transaction files, SYSTEM registry transaction files, Setupapi.log Win7+, Setupapi.log Win7+, Setupapi.log XP, Syscache, Syscache transaction files, System Profile registry hive, System Profile registry hive, System Profile registry transaction files, System Profile registry transaction files, System Restore Points Registry Hives (XP), Thumbcache DB, UsrClass.dat registry hive, UsrClass.dat registry transaction files, WindowsIndexSearch, XML, XML, at .job, at .job, at SchedLgU.txt, at SchedLgU.txt
```

Yields a ZIP 100,000 KB for my Desktop

Select in Config params

The triage zip file can then be downloaded from browser

#### 2. Event Logs

Event log collection works fine on home desktop.

- json file
- excel file

- Export these into
  - Axiom has log event viewer
  - Splunk
  - Elastic Search (SOFELK)

#### 3. All running processes, DLLs
---
title: Splunk
parent: Tools
has_children: true
nav_order: 8
---
As memory is large on servers capturing memory is not best way of capturing volatile state as it takes so long so have some alternatives similar to *volatility*

##### Mutants
Malware typically need to persist using multiple persistance mechanisms - in case one mechanism is detected and removed, often other mechanisms will re-infect the machine. This leaves a common problem: How to avoid multiple copies of the same malware from running?

A common solution is using a Mutant or a named mutex object. A Mutant is a named kernel object that can only be “acquired” by one thread at a time. Multiple copies of the same malware will try to acquire the mutant, but only the first will succeed, leaving the rest to exit.

For this reason, a mutant is frequently used as an indicator for a malware strain because it is easy to see if the mutant name exists on a system. 

Enumerate the mutants
You can enumerate the mutant using the `Windows.Detection.Mutants` artifact. This artifact can be used to collect all mutants (and perhaps do some analysis on their names) or to check for some well known names using a filter (in which case a hit represents a strong signal that endpoint is compromised).

```PowerShell
$createdNew = $False
$mutex = New-Object -TypeName System.Threading.Mutex(
      $true, "Global\MyBadMutex", [ref]$createdNew)
if ($createdNew) {
    echo "Acquired Mutex"
    sleep(1000)
} else {
    echo "Someone else has the mutex"
}
```

- Run in powershell.. `Acquired Mutex`. 
- Run again in another window... `Someone else has the mutex`... can only run once

An important principle of volatile system analysis is to disturb the system as little as possible, to avoid increasing the rate at which the volatile evidence might change. A full memory acquisition defeats this requirement by causing a very large amount of data to be written and potentially transferred over the network. Some server class machines (or even high end workstations) currently contain so much memory that full acquisition is actually not practical (e.g. upwards of 64Gb of RAM is not uncommon), and produces significant amounts of smear.

Velociraptor’s approach is to use the relevant APIs to acquire volatile artifacts as much as possible, so the acquisition can be made quickly, accurately and with minimal endpoint impact. Velociraptor tries to maintain the same names for the common plugins used by popular memory analysis tools like Volatility, but gets the same information using APIs (e.g. Velociraptor’s plugins are named pslist, vad, mutants etc and parallel Volatility’s plugins of the same name).


#### 4. Perimeter logs (We can apparently embed exe in velo)

- VPN logs
- Firewall logs
- How did Thomas collect these?

#### 5. Offline Collector

[Offline Triage](https://docs.velociraptor.app/docs/offline_triage/)

Often we rely of an external helper (such as a local admin) to actually perform the collection for us. However, these helpers are often not DFIR experts. We would like to provide them with a solution that performs the required collection with minimal intervension - even to the point where they do not need to type any command line arguments.

The Offline collector aims to solve this problem. Velociraptor allows the user to build a specially configured binary (which is actually just a preconfigured Velociraptor binary itself) that will automatically collect the artifacts we need.

Velociraptor allow us to build such a collector with the GUI using an intuitive process.

Server Artifacts > Build offline collector > Choose the artifacts we want (e.g., Kape, baisc collection etc)

Choose password for zip folder. This zip will contain another zip folder data.zip.

Launch... Will take a 30s or so. Then we have a zip to download...

C:\Users\danie\Downloads\server-F.C53S8K2U9V98E\
Binary located at sub directory clients\_\collections\F.C53S8K2U9V98E\uploads

It is easily available from Uploaded Files tab.

Can be clicked on to receive executable, run as administrator. Likely to be flagged by AV etc... Run anyway.

##### Importing collections 
1. Into the GUI
We can use the offline collector to fetch multiple artifacts from the endpoint. The results consist of bulk data as well as JSON file containing the result of any artifacts collected.

You can re-import these collection into the GUI so you can use the same notebook port processing techniques on the data. It also allows you to keep the results from several offline collections within the same host record in the Velociraptor GUI.

Offline collection + Import is very similar to client/server except that instead of the client connecting over the internet, the data is delivered via sneakernet!

Importing an offline collection can be done via the Server.Utils.ImportCollection artifact. This artifact will inspect the zip file from a path specified on the server and import it as a new collection (with new collection id) into either a specified client or a new randomly generated client.

NOTE: This artifact reads the collection ZIP from the server’s filesystem. It is up to you to arrange for the file to be stored on the server (e.g. scp it over).

The above upload method didnt work (although the collection did)

2. With ShareFile

Will output a zip file to same directory as executable. Local admin can upload to *ShareFile* for us.

*NOT DONE THIS TRY* Collecting across the network
By having a single executable collector, all we need is to run it remotely. We can use another EDR solution that allows remote execution if available. Alternatively, we can use Window’s own remote management mechanisms (such as PsExec or WinRM) to deploy our binary across the network. Simply, copy our collector binary across the network to C$ share on the remote system and use, e.g. wmic to launch our binary on the remote host.

#### 7. Include third party binaries
Sometimes we want to collect the output from other third party executables. It would be nice to be able to package them together with *velociraptor* and include their output in the collection file.

Velociraptor fully supports incorporating external tools. When creating the offline collection, *velociraptor* will automatically pack any third party binaries it needs to collect the artifacts specified.

