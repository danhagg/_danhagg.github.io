---
title: Power User
parent: Splunk
grand_parent: Certifications
nav_order: 2
---

# Power User

## Introduction
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

## SPL

- Command modifiers (Orange)
- Commands (Blue)
- Arguments (Green)
- Functions (Purple)

```markdown
| stats sum(bytes) as Total\_Bytes
| eval Total\_bytes = tostring(Total\_Bytes, “commas”)
```

```markdown
index=web
| table clientIP, action, categoryId, status
| where isnotnull(action)
| rename action as “ACTION”, clientIP as “Shoppers IP”
| fields - status
```

Transforming commands order results into a data table

*Top* vs *rare (Top 10 vs Rarest 10)*

index=security \*fail\* | top src showperc=f
| rare limit=1 fieldName
| stats count by fieldName
|stats values(referrer domain)
| stats count by referrer domain, action
| stats values(usr) as “Login Name”, count(user) as “Attempts” by src
| fillnull value="No Data available"

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
