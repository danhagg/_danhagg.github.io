---
title: Account Usage
parent: Windows Artifacts
has_children: true
nav_order: 6
---

# Account Usage

## Authentication Events
Local/Account Workgroup = on workstation
Domain/Active Directory = on domain controller
_%SYSTEM ROOT%\System32\winevt\logs\Security.evtx_
- NTLM Protocol
    - 4776: Successful/Failed account authentication
- Kerberos
    - 4768: Ticket Granting Ticket was granted (successful logon)
    - 4769: Service ticket requested (access to server resource)
    - 4771: Pre-authentication failed (failed logon)

## Last login
_C:\windows\system32\config\SAM_
_SAM\domains\Account\Users_
- List local accounts and SID
- Only last login time will be stored

## Last Password Change
_C:\windows\system32\config\SAM_
_SAM\domains\Account\Users_
- Lists last time the password of a specific local user has been changed	

## Logon Types
_Security.evtx_

Event ID’s
- 4624 - Successful Logon

Logon Type 		Explanation
2 		Logon via console
3 		Network Logon
4 		Batch Logon
5 		Windows Service Logon
7 		Credentials used to unlock screen (*also reconnect)
8 		Network logon sending credentials (cleartext)
9 		Different credentials used than logged on user
10 		Remote interactive logon (RDP)
11 		Cached credentials used to logon
12 		Cached remote interactive (similar to Type 10)
13 		Cached unlock (similar to Type 7)

- 4625        Failed Logon
- 4634/4647   Successful logoff
- 4648        Logon using explicit credentials (Runas)
- 4672        Account logon with superuser rights (Administrator)
- 4720        An account was created

## RDP Usage

### RDP Successful Logon
ID	    Message	Location
1149	User authentication succeeded (connection)	MWTS-RemoteConnectionManager%4Operational.evtx
4624    (7*,10)	An account successfully logged on (authentication)	Security.evtx
21	    RDServices: Session logon succeeded (logon)	MWTS-RemoteConnectionManager%4Operational.evtx
22	    RDServices: Shell start logon notification received (logon)	MWTS-RemoteConnectionManager%4Operational.evtx

- 7* reconnect

###	RDP Unsuccessful Logon
ID	    Message	Location
1149	User authentication succeeded (connection)	MWTS-RemoteConnectionManager%4Operational.evtx
4624    (7*,10)	An account failed to logon (authentication)	Security.evtx

###	RDP Session Disconnect (Window close)
ID	    Message	Location
24	    RDServices: Session has been disconnected	MWTS-RemoteConnectionManager%4Operational.evtx
40	    Session <X> has been disconnected, reason code <Z>	MWTS-RemoteConnectionManager%4Operational.evtx
4779	A session was disconnected from a Window station	Security.evtx
4634	An account was logged off	Security.evtx

###	RDP Session Disconnect (Purposeful: Start > Disconnect)
ID	    Message	Location
24	    RDServices: Session has been disconnected	MWTS-RemoteConnectionManager%4Operational.evtx
39	    Session <X> has been disconnected, reason code <Z>	MWTS-RemoteConnectionManager%4Operational.evtx
40	    Session <X> has been disconnected, reason code <Z>	MWTS-RemoteConnectionManager%4Operational.evtx
4779	A session was disconnected from a Window station	Security.evtx
4634	An account was logged off	Security.evtx

###	RDP Session Reconnect
ID	    Message	Location
1149	User authentication succeeded (connection)	MWTS-RemoteConnectionManager%4Operational.evtx
4624    (7)	An account successfully logged on (authentication)	Security.evtx
25	    RDServices: Session reconnection succeeded	MWTS-RemoteConnectionManager%4Operational.evtx
40	    Session <X> has been disconnected, reason code <Z>	MWTS-RemoteConnectionManager%4Operational.evtx
4778	A session was reconnected to a Window station	Security.evtx

###	RDP Session Logoff
ID	    Message	Location
23	    RDServices: Session logoff succeeded	MWTS-RemoteConnectionManager%4Operational.evtx
4634    (7*, 10)	An account was logged off	Security.evtx
4647	User initiated logoff	Security.evtx
9009	The Desktop Window manager has exited with code <X>	Security.evtx

### Services Events
_System.evtx_
_Security.evtx_

- Malware and Worms often utilize services
- Services started on boot illustrate persistence
- Services can crash due to attacks like process injection
- _System.evtx_
    - 7034 – Service crashed unexpectedly
    - 7035 – Service sent a Start/Stop control
    - 7036 – Service started or stopped
    - 7040 – Start type changed (Boot | On Request | Disabled)
    - 7045 – A service was installed on the system (Win2008R2+)
- _Security.evtx_
    - 4697 – A service was installed on the system

### User Accounts	
_\SAM\SAM\Domains\Account\Users\000003E8\ - RID 1000_
KEYS: _ForcePasswordReset, UserPasswordHint, InternetUserName, InternetProviderGUID, GivenName, Surname, InternetSID, InternetUID, ComplexityPolicy, ComplexityLastUsed, F key, V key_
