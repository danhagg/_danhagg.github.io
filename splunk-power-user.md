---
title: "Fundamentals and Power User"
parent: Splunk
grand_parent: Certifications
nav_order: 1
---


1. # **Fundamentals 1**
dhaggerty PP1..4!@

uname 5plunkbcup

1. ## **Install**
**Linux**

- Can download the appropriate package or use wget (especially for cloud)
- Do not install as root user
- Install into opt
- cd /opt/splunk/bin
- ./splunk start --accept-license
  - insert new creds
- ./splunk start
- ./splunk stop
- ./splunk restart
- ./splunk help

**Windows**

GUI

**Mac OSX**

?

**Cloud**

- As a subscription service
- Removes the infrastructure requirements from you

**Apps & Roles**

- Apps are preconfigured environments, workspaces designed to solve certain problems

1. ## **Components**
**Indexers**

indexes an event in a directory (by age)

**Search Head**

Search request from users. Queries indexers and returns data to user

**Forwarders**

Splunk enterprise instances consuming data and forwarding to indexers. Reside on machines where data generated.

1. ## **Bits**
Single instance of Splunk:

- Input
- Parsing
- Indexing
- Searching

Roles

- Admin
- Power user
- user

Data Ingestion choices

- Upload
  - Great for testing
  - Name of machine logs collected from
- Monitor
  - Files and directories
  - HTTP
  - TCP/UDP
  - Scripts
- Forward

Multiple indexes

- Allows searching over smaller data size can store indexes over different lengths of time

Commands that create statistics and visualizations are called **transforming** commands.

By default, a search job will remain active for 10 minutes

Search modes

- fast
- smart
- verbose

1. ## **Events**
**Searches**

- In order of evaluation
- NOT, OR, AND
- AND is implied if not stated
  - e.g., port 22 vs “port 22”

failed NOT (success OR accepted)

- \” - escapes quotations so you can search for them
- \* wildcard
- Job settings: searches saved for 7 days
- Drag a bookmark icon to browser

**Selected fields**

- host
- source 
- sourcetype

**Interesting fields**

\>20% search results

**Data types**

a - string

\# - numerical

field names are case sensitive values are not

=, != (string and numerical)

\>, >=, <, <= (numerical)

index=webstatus IN (“200”, “304)

**Best practices of searching/filtering**

- time
- index\*
- source\*
- host\*
- sourcetype\*

\*Extracted at index time

- The more specific the better. 
- Inclusion > exclusion.
- Filter early in commands to limit events

**Time**

Real-time searches

10 mins ago to now

-30m, -30s, (s, m, h, d, w, mon, y)

sourcetype=access\_combined earliest=-2h latest=-1h

sourcetype=access\_combined earliest=01/01/2021

index=web OR ma\*

**Splunk Search Language (SPL)**

Five components

- Search terms
- Commands
  - Charts, stats, formulas
- Functions
  - How we want to chart, compute, evaluate
- Arguments
  - Variables that go into functions
- Clauses
  - Explain how we want results, grouped, defined

sourcetype=acc\* | stats list(prod\_nam) **as** “Games Sold”

CTRL + \ puts pipes on new line

1. ## **Commands**

**Field**

- Field inclusion happens before field extraction and can improve performance
- Field exclusion happens after field extraction only affecting displayed results

| fields status clientip

| fields - status clientip

**Table**

- display results in simple table

| table JSESSIONID, product\_name, price

**Rename**

- New field names will need to be used further down the pipeline

| rename JSESSIONID as “User Session”

**Dedup**

- deduplicate on a field

| dedup username

**Sort**

- New field names will need to be used further down the pipeline

| table vendor product\_name sale\_price

| sort vendor sale\_price limit=20

`	`vs

| sort - sale\_price vendor limit=20 (desc)

| sort -sale\_price vendor limit=20 (desc just sale\_price)

1. ## **Transform Commands**
Order search results into a data table for statistical purposes

**Top**

Most common values of a given field

| top vendor limit=20 

showperc=False

countfield=”Number of Sales”

useother=True

Use **top** to split **by** a second field

| top product\_name by vendor limit=3

**Rare**

- Reverse of top
- Uses same clauses as Top

**Stats**

- count
- distinct\_count or dc
- sum
- average or avg
- min
- max
- list
- values

| stats count as “Total” by product\_name, sales\_price

| stats count(action) as “Action Events”, count as “Total Events”

field passed as argument to count function

| stats distinct\_count(product\_name) as “Number of games for sale by vendors” by sale\_price

| stats sum(price) as “Gross Sales” by product\_name

| stats count as “Units sold” sum(price) as “Gross Sales” by product\_name

| stats avg(field\_price) as “Average Price) 

min(sales-price) as “Min Price” 

max(sales\_price) as “max Price” by category\_id

**List**

List all values of a given field

| stats list(Asset) as “Company Assets” by Employee

**Questions**

host=web\_application file=cart.do OR success.do status=200 | stats count by file | rename count as "Transactions" file as "Functions"

**How many logins**

host=web\_application | stats dc(JSESSIONID)

**How many bytes (bytes = field name)**

host=web\_application status=200 | stats sum(bytes) as TotalBytes by file | sort TotalBytes

**Find long query times**

index=\* Command=\* | stats avg(Duration) as "Query Time" by Command | sort -"Query Time"

**Sort by most common browser**

index=\* useragent=\* | stats count(useragent) by useragent | sort -count(useragent)

**Sort by most common ips forbidden page**

index=main status="403" | stats count as Attempts by clientip | sort -Attempts

1. ## **Reports & Dashboards**

**Reports**

- Are saved searches
- Save As > report 
- naming convention: Group\_type\_description

**Visualizations**

Save As Report or Dashboard

Add a Time Ranger Picker

- Edit
- Add input
- Time
- Edit
  - Label: time Range
  - Search on Change (tick)
  - Token: TimeRangePkr

Time range picker only works on panels with an inline search

e.g., Go to choropleth (search) 

- click & clone to inline
- click again
- Time Range
- Shared Time Picker
- TimeRangePkr

Repeat for all panels you want driven by TimeRangePkr 

1. ## **Pivot & Datasets**

- Pivot
- Instant pivot
- datasets

**Pivot**

Can create reports without search strings

**Data Models**

- Are knowledge objects that provide the data structure that drives pivots created by admin and power roles.
- Data models are mase up of Datasets.

**Datasets**

- Tables
  - Fieldnames for columns
  - Values for cells

ROOT OBJECT

sourcetype=access\_combined

CHILD OBJECT

status=200

CHILD OBJECT

action=purchase

CHILD OBJECT

stats count by product\_name

1. ## **Lookups**

Lookups allow you to add other fields and values to your events not included in the indexed data

- csv file
- scripts
- geospatial data

You can configure your lookup to run automatically

A lookup is characterized as a dataset. Two steps to setup a lookup file

1. Define a lookup table
1. Define the lookup

e.g., if we want to convert status field in data from numbers (200 etc) to a description.

http\_status.csv

code, description

200, OK

**Put file in Splunk (method 1)**

add http\_status.csv to

C:\Program Files\Splunk\etc\apps\search\lookups

check lookup works with

| inputlookup http\_status.csv

**Put file in Splunk (method 2)**

- Settings
- Lookups
- Destination App: Search
- Destination filename: http\_status.csv

**Define Lookup**

- Settings
- Lookups
- Lookup definitions
- Add new
  - Destination App: search
  - Name: http\_status
  - Type: file-based
  - lookup file: http\_status.csv

**Lookup command**

| lookup http\_status code as status

**Output clause**

index=\* | lookup http\_status code as status,

OUTPUT code as "HTTP Code",

description as "HTTP Description"

| table host, "HTTP Code", "HTTP Description"

**Automatic Lookups**

- Settings
- Lookups
- Automatic Lookups
- Add new

Destination App: search

Name: http\_status\_lookup

Lookup table: http\_status\_lookup

input fields: code = status

output fields: code = Code

description = Description

**Additional lookup options**

- Populate lookup table with search results
- Define lookup based on external script or command
- Use Splunk DB connect application
- Use geospatial lookups to create queries > choropleth map visualizations
- populate events with KV store fields

**Lookup Quiz**

file=success.do status=200 | lookup products\_lookup productId as productId OUTPUT product\_name as ProductName | stats count as Total by ProductName

1. ## **Scheduled Reports**
**Triggers an action each time it runs**

Useful for:

- Weekly/Monthly reports
- Dashboards
- Sending reports by email
  - <https://community.splunk.com/t5/Alerting/How-to-configure-my-email-settings-to-get-email-alert/m-p/231540>

Search> Save As > report

- As the report is scheduled do NOT pick a time range

Schedule priority (Admin required)

- Windows=Auto

Add actions

- Log event
- Output results to lookup
- Output results to a telemetry endpoint
- Run a script
- Send email
- Webhook

Can also build custom actions

Edit > Embed: Can be viewed by anyone

Yields an iframe

**Alerts**

Based on searches that run on scheduled intervals or real time.

Notify you when the results of a search meet defined conditions

Alerts triggered when the search is finished

Alerts can:

- List in the interface
- Log events
- Output to a lookup
- Send to a telemetry endpoint
- Trigger scripts
- Send emails
- Use a webhook
- Run a custom alert

Trigger alert

- Per result
- Number of results
- Number of hosts
- Number of sources
- Custom

1. ## **Miscellaneous**

**View source data**

| eventcount summarize=false index=\* | dedup index

**View Index metadata**

| metadata type=sources index=\*

1. # **Power User**
   1. ## **Introduction**
Three core components:

- forwarders
- indexers
- search heads

Deployments

- Standalone (Single instance, no forwarders)
- Basic (Can use forwarders)
- Multi-instance (Functional separation of Search Heads, indexers)

Deployment server for deploying multiple forwarders

Input types

- Upload
- Monitor (Files/Ports on this Splunk instance)
- Forward Data from Splunk Forwarder

Input Phase

- Source: Path of data, method of collection
- Host: Who sent data
- Source type: Data format, Linux secure

Knowledge Object

<group name>\_<type>\_<description>

Fields are case sensitive

Values are not case sensitive



**categoryId!=SPORTS**

Exclude events where categoryId does not include SPORTS

**NOT categoryId=SPORTS**

Same as above PLUS exclude events with no categoryId entry

1. ## **SPL**
- Command modifiers (Orange)
- Commands (Blue)
- Arguments (Green)
- Functions (Purple)

| stats sum(bytes) as Total\_Bytes

| eval Total\_bytes = tostring(Total\_Bytes, “commas”)

index=web

| table clientIP, action, categoryId, status

| where isnotnull(action)

| rename action as “ACTION”, clientIP as “Shoppers IP”

| fields - status

Transforming commands order results into a data table

*Top* vs *rare (Top 10 vs Rarest 10)*

index=security \*fail\* | top src showperc=f

| rare limit=1 fieldName

| stats count by fieldName

|stats values(referrer domain)

| stats count by referrer domain, action

| stats values(usr) as “Login Name”, count(user) as “Attempts” by src

| fillnull value=”No Data available”

index=\_internal

| eval epoch\_time=strptime(\_time, “%s”)

| eval hrt=strftime(epoch\_time, “%m/%d/%y %H:%M”)

| table \_time, epoch\_time, hrt

index=web

| eval status\_codes=case((status==404), “not found”, (status==400), “bad request”,)

| stats count by status, status\_codes

index=web

| stats count(eval(status==404)) as “number of founds”

| eval hash=md5(file)

index=security

| table src, user, action

| where like(src, “64.%)

| search user=bob





`		     `Page  **PAGE  \\* Arabic  \\* MERGEFORMAT 1** of  **NUMPAGES  \\* Arabic  \\* MERGEFORMAT 2**
