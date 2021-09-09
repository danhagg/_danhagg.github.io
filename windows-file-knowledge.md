---
title: File Knowledge
parent: Windows Artifacts
has_children: true
nav_order: 5
---

# File Knowledge

## File Download
ADS Zone.Identifier
`Get-Item * -Stream zone*`
- NTFS Alternate Data Stream: When files are downloaded from the Internet Zone via browser to NTFS an alternate data stream is added to the file

### Browser Downloads
_C:\Users\<profile>\AppData\Local\Google\Chrome\UserData\Default\history_
_C:\Users\<profile>\AppData\Roaming\Mozilla\Firefox\Profiles\<random>\places.sqlite_

### Email Attachments
_C:\Users\<profile>\AppData\Local\Microsoft\Outlook_
- Emails allow standard text
- Attachments must be encoded with MIME/base64 format
- Outlook data files found in .ost and .pst

### Open/Save MRU
_NTUSER.dat\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSavePidMRU_
- Key tracks files that have been opened or saved within a Windows shell dialog box
- Keys in registry:
    - *: recent files
    - ext: by extension (e.g., ppt)

## Deleted File or File Knowledge
### Thumbcache
_C:\Users\<profile>\AppData\Local\Microsoft\Windows\Explorer_
- Thumbnails of pictures, office docs and folders exist in thumbcache.
- Created when a user switches a folder to thumbnail mode or views pictures via a slideshow

### Thumbs.db
Automatically created anywhere and accessed via UNC path
- Hidden file in directory where images on machine exist stored in a smaller thumbnail graphics. 
- thumbs.db catalog pictures in a folder and stores a copy of thumbnail even if the pictures were deleted.

### IE|Edge file://
_C:\Users\<profile>\AppData\Local\Microsoft\Windows\WebCache\WebCacheV*.dat_
- IE History also records local and remote file access
- Stored in index.dat as file:///C:/directory/filename.ext

### Search - WordWheelQuery
_NTUser.dat_ hive
_NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\WordWheelQuery_
- Keywords searched from the START menu bar 

### Recycle Bin
_C:\$Recycle.bin_
- Original Path/name
- Deletion date/time

### Jump lists
_C:\Users\<profile>\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations_
- Task bar == Jump list
- AutomaticDestinations: unique file prepended with the AppID embedded with LNK files in each stream
- Using the Structured Storage Viewer, open up one of the AutomaticDestination jump list.
- Each one of these files is a separate LNK file. Stored numerically earliest (1) to the most recent.

### Last-Visited MRU
_NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\LastVisitedPidIMRU_
- Tracks specific executable used by an application to open the files documented in OpenSaveMRU key
- Each value also tracks the direction location for the last file accessed by that application
- e.g., notepad.exe was last run using the C:\Users\dan\Desktop folder

### Office Recent Files
NTUSER.DAT\Software\Microsoft\Office\16.0\Excel\User MRU\####HASH####\File MRU
- Office programs track their own recent files list-> users to remember what files they were editing
- In my registry 1st key was most recently opended

### Open/Save MRU
_NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSavePidIMRU_
- Tracks files that have been opened or saved within Windows Shell dialog box
- The * key: This subkey tracks the most recent files of any extension input in OpenSave dialog
- ??? (three letter extension) - This subkey stores file info from the OpenSave dialog by specific extension.
    - .??? => Subkey stores the temporal order last files opened with this extension
    - Folder => Subkey stores the temporal order last files

### Prefetch files
_C:\Windows\Prefetch_
- Increases system performance by preloading code pages of commonly used applications
- Cache manager monitors files/directories refd for each application/process & maps them to a .pf file
- Utilized to know an application was executed on a system
- exename-hash.pf
- We can examine each .pf file to look for file and device handles recently used

### Recent Files
_NTUSER.DAT\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs_
- Registry Key tracks last files/folders opened & used to populate data in Recent menus of the Start menu.
- The overall key tracks in temporal order last 150 files/folders opened

### Shellbags
NTUSER.DAT
- _Local Settings\Software\Microsoft\Windows\Shell\Bags_
- _Local Settings\Software\Microsoft\Windows\Shell\BagsMRU_
- Stores information about which folders were most recently browsed by the user

### Shortcut (LNK) files
_C:\Users\<profile>\AppData\Roaming\Microsoft\Windows\Recent_
- Shortcut files automatically created by Windows when opening local & remote files
- Creation date of LNK file
- Last modification date of LNK file
