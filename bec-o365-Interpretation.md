---
title: O365 Interpretation
parent: O365 Audit Logs
grand_parent: Business Email Compromise
nav_order: 4
---

# O365 Interpretation

### Property
- Description

_Microsoft 365 service_

### Actor
- The user or service account that performed the action.

_Azure Active Directory_

### AddOnName
- The name of an add-on that was added, removed, or updated in a team. The type of add-ons in Microsoft Teams is a bot, a connector, or a tab.
_Microsoft Teams_

### AddOnType
- The type of an add-on that was added, removed, or updated in a team. The following values indicate the type of add-on.
- 1 - Indicates a bot.
- 2 - Indicates a connector.
- 3 - Indicates a tab.
_Microsoft Teams_

### AzureActiveDirectoryEventType
- The type of Azure Active Directory event. The following values indicate the type of event.
- 0 - Indicates an account login event.
- 1 - Indicates an Azure application security event.
_Azure Active Directory_

### ChannelGuid
- The ID of a Microsoft Teams channel. The team that the channel is located in is identified by the TeamName and TeamGuid properties.
_Microsoft Teams_

### ChannelName
- The name of a Microsoft Teams channel. The team that the channel is located in is identified by the TeamName and TeamGuid properties.
_Microsoft Teams_

### Client
- The client device, the device OS, and the device browser used for the login event (for example, Nokia Lumia 920; Windows Phone 8; IE Mobile 11).
_Azure Active Directory_

### ClientInfoString
- Information about the email client that was used to perform the operation, such as a browser version, Outlook version, and mobile device information
_Exchange (mailbox activity)_

### ClientIP
- The IP address of the device that was used when the activity was logged. The IP address is displayed in either an IPv4 or IPv6 address format.
- For some services, the value displayed in this property might be the IP address for a trusted application (for example, Office on the web apps) calling into the service on behalf of a user and not the IP address of the device used by person who performed the activity.
- Also, for admin activity (or activity performed by a system account) for Azure Active Directory-related events, the IP address isn't logged and the value for the ClientIP property is null.
_Azure AD, Exchange, SharePoint_

### CreationTime
The date and time in Coordinated Universal Time (UTC) when the user performed the activity.
_All_

### DestinationFileExtension
- The file extension of a file that is copied or moved. This property is displayed only for the FileCopied and FileMoved user activities.
_SharePoint_

### DestinationFileName
- The name of the file is copied or moved. This property is displayed only for the FileCopied and FileMoved actions.
_SharePoint_

### DestinationRelativeUrl
- The URL of the destination folder where a file is copied or moved. The combination of the values for the SiteURL, the DestinationRelativeURL, and the DestinationFileName property is the same as the value for the ObjectID property, which is the full path name for the file that was copied. This property is displayed only for the FileCopied and FileMoved user activities.
_SharePoint_

### EventSource
- Identifies that an event occurred in SharePoint. Possible values are SharePoint and ObjectModel.
_SharePoint_

### ExternalAccess
- For Exchange admin activity, specifies whether the cmdlet was run by a user in your organization, by Microsoft datacenter personnel or a datacenter service account, or by a delegated administrator. The value False indicates that the cmdlet was run by someone in your organization. The value True indicates that the cmdlet was run by datacenter personnel, a datacenter service account, or a delegated administrator.
- For Exchange mailbox activity, specifies whether a mailbox was accessed by a user outside your organization.
_Exchange_

### ExtendedProperties
- The extended properties for an Azure Active Directory event.
_Azure Active Directory_

### ID
- The ID of the report entry. The ID uniquely identifies the report entry.
_All_

### InternalLogonType
- Reserved for internal use.
_Exchange (mailbox activity)_

### ItemType
- The type of object that was accessed or modified. Possible values include File, Folder, Web, Site, Tenant, and DocumentLibrary.
_SharePoint_

### LoginStatus
- Identifies login failures that might have occurred.
_Azure Active Directory_

### LogonType
- The type of mailbox access. The following values indicate the type of user who accessed the mailbox.
- 0 - Indicates a mailbox owner.
- 1 - Indicates an administrator.
- 2 - Indicates a delegate.
- 3 - Indicates the transport service in the Microsoft datacenter.
- 4 - Indicates a service account in the Microsoft datacenter.
- 6 - Indicates a delegated administrator.
_Exchange (mailbox activity)_

### MailboxGuid
- The Exchange GUID of the mailbox that was accessed.
_Exchange (mailbox activity)_

### MailboxOwnerUPN
- The email address of the person who owns the mailbox that was accessed.
_Exchange (mailbox activity)_

### Members
- Lists the users that have been added or removed from a team. The following values indicate the Role type assigned to the user.
- 1 - Indicates the Owner role.
- 2 - Indicates the Member role.
- 3 - Indicates the Guest role.
- The Members property also includes the name of your organization, and the member's email address.
_Microsoft Teams_

### ModifiedProperties (Name, NewValue, OldValue)
- The property is included for admin events, such as adding a user as a member of a site or a site collection admin group. The property includes the name of the property that was modified (for example, the Site Admin group) the new value of the modified property (such the user who was added as a site admin, and the previous value of the modified object.
_All (admin activity)_

### ObjectId
- For Exchange admin audit logging, the name of the object that was modified by the cmdlet.
- For SharePoint activity, the full URL path name of the file or folder accessed by a user.
- For Azure AD activity, the name of the user account that was modified.
_All_

### Operation
- The name of the user or admin activity. The value of this property corresponds to the value that was selected in the Activities drop down list. If Show results for all activities was selected, the report will included entries for all user and admin activities for all services. For a description of the operations/activities that are logged in the audit log, see the Audited activities tab in Search the audit log in the Office 365.
- For Exchange admin activity, this property identifies the name of the cmdlet that was run.
_All_

### OrganizationId
- he GUID for your organization.
_All_

### Path
- The name of the mailbox folder where the message that was accessed is located. This property also identifies the folder a where a message is created in or copied/moved to.
_Exchange (mailbox activity)_

### Parameters
- For Exchange admin activity, the name and value for all parameters that were used with the cmdlet that is identified in the Operation property.
_Exchange (admin activity)_

### RecordType
The type of operation indicated by the record. This property indicates the service or feature that the operation was triggered in. For a list of record types and their corresponding ENUM value (which is the value displayed in the RecordType property in an audit record), see Audit log record type.


### ResultStatus
- Indicates whether the action (specified in the Operation property) was successful or not.
- For Exchange admin activity, the value is either True (successful) or False (failed).
_All_

### SecurityComplianceCenterEventType
- Indicates that the activity was a Security & Compliance Center event. All Security & Compliance Center activities will have a value of 0 for this property.
_Security & Compliance Center_

### SharingType
- The type of sharing permissions that was assigned to the user that the resource was shared with. This user is identified in the UserSharedWith property.
_SharePoint_

### Site
- The GUID of the site where the file or folder accessed by the user is located.
_SharePoint_

### SiteUrl
- The URL of the site where the file or folder accessed by the user is located.
_SharePoint_

### SourceFileExtension
- The file extension of the file that was accessed by the user. This property is blank if the object that was accessed is a folder.
_SharePoint_

### SourceFileName
- The name of the file or folder accessed by the user.
_SharePoint_

### SourceRelativeUrl
- The URL of the folder that contains the file accessed by the user. The combination of the values for the SiteURL, the SourceRelativeURL, and the SourceFileName property is the same as the value for the ObjectID property, which is the full path name for the file accessed by the user.
_SharePoint_

### Subject
- The subject line of the message that was accessed.
_Exchange (mailbox activity)_

### TabType
- The type of tab added, removed, or updated in a team. The possible values for this property are:
    - Excel pin - An Excel tab.
    - Extension - All first-party and third-party apps; such as Class Schedule, VSTS, and Forms.
    - Notes - OneNote tab.
    - Pdfpin - A PDF tab.
    - Powerbi - A Power BI tab.
    - Powerpointpin - A PowerPoint tab.
    - Sharepointfiles - A SharePoint tab.
    - Webpage - A pinned website tab.
    - Wiki-tab - A wiki tab.
    - Wordpin - A Word tab.
_Microsoft Teams_

### Target
- The user that the action (identified in the Operation property) was performed on. For example, if a guest user is added to SharePoint or a Microsoft Team, that user would be listed in this property.
_Azure Active Directory_

### TeamGuid
- The ID of a team in Microsoft Teams.
_M_icrosoft Teams_

### TeamName
- The name of a team in Microsoft Teams.
_Microsoft Teams_

### UserAgent
- Information about the user's browser. This information is provided by the browser.
_SharePoint_

### UserDomain
- Identity information about the tenant organization of the user (actor) who performed the action.
_Azure Active Directory_

### UserId
- The user who performed the action (specified in the Operation property) that resulted in the record being logged. Audit records for activity performed by system accounts (such as SHAREPOINT\system or NT AUTHORITY\SYSTEM) are also included in the audit log. Another common value for the UserId property is app@sharepoint. This indicates that the "user" who performed the activity was an application that has the necessary permissions in SharePoint to perform organization-wide actions (such as search a SharePoint site or OneDrive account) on behalf of a user, admin, or service. For more information, see The app@sharepoint user in audit records.
_All_

### UserKey
- An alternative ID for the user identified in the UserID property. For example, this property is populated with the passport unique ID (PUID) for events performed by users in SharePoint. This property also might specify the same value as the UserID property for events occurring in other services and events performed by system accounts.
_All_

### UserSharedWith
- The user that a resource was shared with. This property is included if the value for the Operation property is SharingSet. This user is also listed in the Shared with column in the report.
_SharePoint_

### UserType
- The type of user that performed the operation. The following values indicate the user type.
_All_








0 - A regular user.




2 - An administrator in your Microsoft 365 organization.1




3 - A Microsoft datacenter administrator or datacenter system account.




4 - A system account.




5 - An application.




6 - A service principal.




7 - A custom policy.




8 - A system policy.


### Version
Indicates the version number of the activity (identified by the Operation property) that's logged.
All

### Workload
The Microsoft 365 service where the activity occurred.
All




### MailItemsAccessed
Messages were read or accessed in mailbox. Audit records for this activity are triggered in one of two ways: when a mail client (such as Outlook) performs a bind operation on messages or when mail protocols (such as Exchange ActiveSync or IMAP) sync items in a mail folder. This activity is only logged for users with an Office 365 or Microsoft 365 E5 license. Analyzing audit records for this activity is useful when investigating compromised email account. For more information, see the "Access to crucial events for investigations" section in Advanced Audit.

### AddMailboxPermissions
An administrator assigned the FullAccess mailbox permission to a user (known as a delegate) to another person's mailbox. The FullAccess permission allows the delegate to open the other person's mailbox, and read and manage the contents of the mailbox.

### UpdateCalendarDelegation
A user was added or removed as a delegate to the calendar of another user's mailbox. Calendar delegation gives someone else in the same organization permissions to manage the mailbox owner's calendar.

### AddFolderPermissions
A folder permission was added. Folder permissions control which users in your organization can access folders in a mailbox and the messages located in those folders.

### Copy
A message was copied to another folder.

### Create
An item is created in the Calendar, Contacts, Notes, or Tasks folder in the mailbox. For example, a new meeting request is created. Creating, sending, or receiving a message isn't audited. Also, creating a mailbox folder is not audited.

### New-InboxRule
A mailbox owner or other user with access to the mailbox created an inbox rule in the Outlook web app.

### SoftDelete
A message was permanently deleted or deleted from the Deleted Items folder. These items are moved to the Recoverable Items folder. Messages are also moved to the Recoverable Items folder when a user selects it and presses Shift+Delete.

### ApplyRecordLabel
A message was classified as a record. This occurs when a retention label that classifies content as a record is manually or automatically applied to a message.

### Move
A message was moved to another folder.

### MoveToDeletedItems
A message was deleted and moved to the Deleted Items folder.

### UpdateFolderPermissions
A folder permission was changed. Folder permissions control which users in your organization can access mailbox folders and the messages in the folder.

### Set-InboxRule
A mailbox owner or other user with access to the mailbox modified an inbox rule using the Outlook web app.

### HardDelete
A message was purged from the Recoverable Items folder (permanently deleted from the mailbox).

### Remove-MailboxPermission
An administrator removed the FullAccess permission (that was assigned to a delegate) from a person's mailbox. After the FullAccess permission is removed, the delegate can't open the other person's mailbox or access any content in it.

### RemoveFolderPermissions
A folder permission was removed. Folder permissions control which users in your organization can access folders in a mailbox and the messages located in those folders.

### Send
A message was sent, replied to or forwarded. This activity is only logged for users with an Office 365 or Microsoft 365 E5 license. For more information, see the "Access to crucial events for investigations" section in Advanced Audit.

### SendAs
A message was sent using the SendAs permission. This means that another user sent the message as though it came from the mailbox owner.

### SendOnBehalf
A message was sent using the SendOnBehalf permission. This means that another user sent the message on behalf of the mailbox owner. The message indicates to the recipient whom the message was sent on behalf of and who actually sent the message.

### UpdateInboxRules
A mailbox owner or other user with access to the mailbox modified an inbox rule in the Outlook client.

### Update
A message or its properties was changed.

### MailboxLogin
The user signed in to their mailbox.

### ?
A user applied a retention label to an email message and that label is configured to mark the item as a record.

