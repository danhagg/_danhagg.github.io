---
title: External Device/USB
parent: Windows Artifacts
has_children: true
nav_order: 7
---

# External Device/USB

## PnP Events
_%system root%\System32\winevt\logs\System.evtx_

- When a PnP driver install is attempted, the service will log an ID 20001 event and provide a Status
- Timestamp
- Device information
- Status (0 = no errors)

## USB Drive Letter & Volume Name
_SOFTWARE\Microsoft\Windows Portable Devices\Devices_
- SYSTEM\MountedDevices

- Examine Drive Letters looking at Value Data Looking for Serial Number
- Discover the last drive letter of the USB Device when it was plugged into the machine.
- Identify the USB device that was last mapped to a specific drive letter. 
- This technique will only work for the last drive mapped. 

## USB First/Last Times
PLUG N PLAY log files: First Time. _C:\Windows\inf\setupapi.dev.log_ (text file)
- Search for Device Serial number
- Log File times are set to local time zone

\CurrentControlSet\Enum\USBSTOR\Ven_Prod_Version\USBSerial#\Properties\{83da6326-97a6-4088-9453-a19231573b29}\####
- 0064 = First Install (Win7-10)
- 0066 = Last Connected (Win8-10)
- 0067 = Last Removal (Win8-10)

## USB Key Identification
_SYSTEM\CurrentControlSet\Enum\USBSTOR_
_SYSTEM\CurrentControlSet\Enum\USB_

- Track USB devices plugged into a machine
- Vendor, product, version, time

## USB Users
Find GUID from SYSTEM\MountedDevices
_NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\MountPoints2_

- The GUID will be used to identify user who plugged in device. 
- Last write time of this key corresponds to the last time device was plugged into the machine by that user.
- The number will be referenced in the user’s personal mountpoints key in the NTUSER.DAT Hive.

## USB Shortcut (LNK) Files
_%USERPROFILE%\AppData\Roaming\Microsoft\Windows_
_%USERPROFILE%\AppData\Roaming\Microsoft\Office\Recent_

- Shortcut files automatically created by Windows
- Recent Items
- Open local and remote data files and documents will generate a shortcut file (.lnk) 
- Date/Time file of that name was first opened
- Creation Date of Shortcut (LNK) File
- Date/Time file of that name was last opened
- Last Modification Date of Shortcut (LNK) File
- LNK Target File (Internal LNK File Information) Data:
- Modified, Access, and Creation times of the target file
- Volume Information (Name, Type, Serial Number)
- Network Share information
- Original Location be same as GUIDs

## USB Volume Serial Number
_SOFTWARE\Microsoft\WindowsNT\CurrentVersion\ENDMgmt_

- Discover the Volume Serial Number of
- Knowing both the Volume Serial Number and the Volume Name, you can correlate the data across SHORTCUT File (LNK) analysis and the RECENTDOCs key.
- The Shortcut File (LNK) contains the Volume Serial Number and Name
- The RecentDocs Registry Key will contain the volume name when the USB device is opened via Explorer

