---
title: O365 Attack
parent: O365 Audit Logs
grand_parent: Business Email Compromise
nav_order: 1
---

# BEC O365 Collections

## Anatomy of Attack

- Bogus invoices
- Business Executive requests
- Fraudulent Correspondence
- Executive/Attorney impersonation
- Data theft

## BEC Attack Old method
- Change domain name
- Get CEO/CFO from LinkedIn
- Send at end of day to be completed immediately
- Fake that its a forward
- Pick lower amounts early on and ramp up
- External domains can now have flagged text

## BEC Attack New method
- Spray out some dubious links to company try and get a click
- Attacker knows this is someone who clicks on emails
- Send another email, maybe a Docusign phish, click on link and user may be presented with a login screen for all the major sign ins, One drive, Google, Microsoft etc
- Once they have that *inbox* creds they know that some people will trust emails from it
- POP3/IMAP
- SMTP 
- protocol is text
- but is extensible (for pics etc)
- All email delivered by SMTP protocol

- User Agent == Email application on client
- Private email system eg Outlook (just on one client not browser based)
- Web based user agent
- MTA message transfer agents (these communicate via SMTP)


## What are we looking for?

- Priority: Is the tenant currently compromised?
- Unauthorized logins?

### Unified Audit Log (UAL)
- Messages are referred to as *objects*
- Much of the logging appears to not be controlled from the web GUI
- PowerShell commands to view logging configuration
- Many operators for AuditOwners (users) may be off by default
    - Create
    - HardDelete
    - MailboxLogin
    - Move
    - MoveToDeletedItems
    - SoftDelete
    - Update

What is PowerShell command to find the audit config. I have a feeling its not viewable in web?

## What is NOT captured in UAL
- Logouts (how long was the bad actor logged in?)
- Length of session
- Messages viewed
- Search terms
- Attachments viewed

## What are we looking for
- Visibility (start/end of logs)
- Locations/IPs
- Logins from non-US countries
- Logins by specific-user non USA
- Logins by not-specific-user non USA (i.e., were other accounts breached)
- Logins from US but not on company site (tricky)
- Time-Travelers (for people within US jumping around locations). (IP location diff)/time = velocity
- If a bad actor has logged in from an IP address, what else has that IP address been doing?
- If a bad actor using VPN client, IP Vanish, anonymizer then IP may jump around
- IP may jump around within a netblock.
- Look for Nigeria
- IMAP/POP3

## Logins
- UserLoggedIn: browser logins generate a lot of this activity
- MailboxLogin:
- PasswordLogonInitialAuthUsingPassword
- ForeignRealmIndexLogonInitialAuthUsingADFSFederatedToken
- PasswordLogonInitialAuthUsingADFSFederatedToken
- ForeignRealmIndexLogonCookieCopyUsingDAToken
- PasswordLogonCookieCopyUsingDAToken

## Mailbox rules
- New-InboxRule (create new inbox rule)
- Set-InboxRule (modifying existing rule)
- Remove-InboxRule
- Set-Mailbox (Account modification)

## If Global Admin account popped
- Add-MailboxPermission
- Add-RecipientPermission
- Set-Mailbox (Account modification)

## Auto-forwarding: 
- Office365 (not in Outlook mail client)
- Options > Mail > Accounts > Forwarding > keep a copy (won’t show up in UAL logs)
- Need to look for using PowerShell (how)
- Need to go into users account and look

[More Office365 Audit Log Info here](https://docs.microsoft.com/en-us/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance?view=o365-worldwide)
