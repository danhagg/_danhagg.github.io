---
title: Velociraptor
parent: Tools
has_children: true
nav_order: 3
---

# Velociraptor

## Deploy locally for testing

```PowerShell
velociraptor config generate -i

velociraptor --config server.config.yaml frontend -v
velociraptor --config client.config.yaml client -v

```

In velociraptor collect kape Basic collection

Select in Config params

Too long path
C:\Users\dhaggerty\OneDrive - The Pronet Group\Velociraptor\self_triage_config

The triage zip file can then be downloaded from browser

## Offline Collector
https://docs.velociraptor.app/docs/offline_triage/

Include third party binaries
Sometimes we want to collect the output from other third party executables. It would be nice to be able to package them together with Velociraptor and include their output in the collection file.

Velociraptor fully supports incorporating external tools. When creating the offline collection, Velociraptor will automatically pack any third party binaries it needs to collect the artifacts specified.

GPO