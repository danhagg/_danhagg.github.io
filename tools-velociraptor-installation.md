---
title: Installation
parent: Velociraptor
grand_parent: Tools
nav_order: 1
---

# Installation

1. Create config files
2. Deploy *velociraptor* and config files to network
3. SCCM or Group Policy to add the MSI to the assigned software group

### *velociraptor* Deployments

#### 1. Generate config files

Download *velociraptor* as MSI to own machine. Add `exe` to PATH.

Use interactive `-i` to generate all sorts of config files for different scenarios and OS.

```PowerShell
velociraptor config generate -i
```

The same *velociraptor* binary can be run as a server or client depending upon which config file it uses: `server` or `client`.

#### 2. Deploy velociraptor,exe and config files to network

- We can use ScreenConnect to access clients network
- Recommeded way of deploying *velociraptor* to clients [here](https://docs.velociraptor.app/docs/deployment/clients/)
  - That is we download *velociraptor* MSI and install (Client IT or ourselves)
  - The advantages are that most enterprise system administration tools are used to deploying software in MSI packages.
  - One of the main benefits in using the official *velociraptor* MSI is that the MSI and the executable are signed. Windows Defender aggressively quarantines unsigned binaries, so it is highly recommended that *velociraptor* be signed.
  - When *velociraptor* starts, it attempts to load the configuration file from `C:\Program Files\Velociraptor\Velociraptor.config.yaml`.
  - Therefore you can use SCCM or Group Policy (see below) to add the MSI to the assigned software group.
  - So to summarise, when installing from the official MSI package you need to:
    - Assign the MSI via Group Policy, or use some other method to deploy the official MSI installer.
    - Copy the configuration file from a share to the *velociraptor* program directory. This can be done via Group Policy Scheduled tasks or another way (see the Group Policy procedure outlined below). As soon as the configuration file is copied, *velociraptor* will begin communicating with the server.
- As we made the `server` and `client` config files in advance we can transfer them via ScreenConnect
- Run velocirator and config files from PowerShell as Administrator

*Note:* When I start *velociraptor* from the following directory `C:\Users\<user>\OneDrive - The Pronet Group\Velociraptor\self_triage_config` I often get a `path too long` warning for some file or other that *velociraptor* collects during triage. In order to avoid this put the `server` and `client` config files with the `velociraptor.exe` in a short-named directory such as `C:\v`.

Run *velociraptor*

```PowerShell
velociraptor --config server.config.yaml frontend -v
velociraptor --config client.config.yaml client -v
```

Visit `https://127.0.0.1:8889` to access *velociraptor* GUI. Accept the SSL warnings.

#### 3. SCCM or Group Policy to add the MSI to the assigned software group
