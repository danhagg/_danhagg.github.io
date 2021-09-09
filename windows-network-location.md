---
title: Network Activity & Physical Location
parent: Windows Artifacts
has_children: true
nav_order: 4
---

# Network Activity & Physical Location

## Timezone
_SOFTWARE\Microsoft\WindowsNT\CurrentVersion\Timezones_
_SYSTEM\ControlSet001\Control\TimezoneInfo_
- In Axiom: Change TZ: Tools > Manage Date/Time format

## Network History
_SOFTWARE\Microsoft\WindowsNT\CurrentVersion\NetworkList\Signatures\Unmanaged_
_SOFTWARE\Microsoft\WindowsNT\CurrentVersion\NetworkList\Signatures\Unmanaged_
_SOFTWARE\Microsoft\WindowsNT\CurrentVersion\NetworkList\Nia\Cache_
- Identify networks computer has been connected to
- Identify domain name/intranet name
- Identify SSID
- Identify Gateway MAC Address
- Will also list networks connected to via VPN

## WLAN Event Log
_Microsoft-Windows-WLAN-AutoConfig Operational.evtx_
- Determine wireless networks system associated with
- Contains SSID and BSSID (MAC address), which can be used to geolocate wireless access point
- 11000 - Wireless network association started
- 8001 - Successful connection to wireless network
- 8002 - Failed connection to wireless network
- 8003 - Disconnect from wireless network
- 6100 - Network diagnostics (System Log)

## System Resource Usage Monitor (SRUM)
_SOFTWARE\Microsoft\WindowsNT\CurrentVersion\SRUM\Extensions_
_SOFTWARE\Microsoft\WlanSvc\Interfaces_
_C:\Windows\System32\SRU_
- Records 30-60 days of historical system performance.
- Applications run, user account responsible for each and bytes sent/received per application per hour

