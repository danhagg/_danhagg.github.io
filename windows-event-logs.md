---
title: Windows Event Logs
parent: Windows Artifacts
has_children: true
nav_order: 3
---

# Event Logs

## Location

_Windows\System32\winevt\Logs_ *.evt *.evtx

## WLAN Event Log
_Microsoft-Windows-WLAN-AutoConfig Operational.evtx_
- Determine wireless networks system associated with
- Contains SSID and BSSID (MAC address), which can be used to geolocate wireless access point
- 11000 - Wireless network association started
- 8001 - Successful connection to wireless network
- 8002 - Failed connection to wireless network
- 8003 - Disconnect from wireless network
- 6100 - Network diagnostics (System Log)