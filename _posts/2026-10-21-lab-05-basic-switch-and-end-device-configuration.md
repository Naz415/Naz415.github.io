---
layout: post
title: "Lab 5: Basic Switch and End Device Configuration (Packet Tracer)"
tags: [module-11, packet-tracer, cisco-ios]
---

**Module:** IT533 Module 11, Cisco IOS basics
**Tools:** Cisco Packet Tracer
**Devices:** Room-145 and Room-146 (2960 switches), Manager and Reception (PCs)
**Time:** 24 minutes (Packet Tracer timer)
**Score:** 98/98 (Packet Tracer counts 28 of 32 items; the other 4 are worth 0 points)

## What the lab asked for

A small LAN with no instructions beyond a requirements list: two switches and two PCs, already cabled and powered. Name both switches, put the same password on every line, set an encrypted enable secret, encrypt the plaintext passwords, add a MOTD banner, address the switch SVIs and the PCs from the addressing table, save, and prove the PCs can reach each other.

The lab hands out one of three name, password and address sets at random. Mine was Room-145 / Room-146 / Manager / Reception on 10.10.10.0/24, line password `8ubRu`, enable secret `C9WrE`.

## What I typed

The commands that ended up in each switch's final config, cleaned up and in order. The full log, every typo included, is in [command-log.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/lab-05/command-log.txt).

Room-145:

```
enable
configure terminal
hostname Room-145
enable password 8ubRu
enable secret C9WrE
line console 0
 password 8ubRu
 login
line vty 0 4
 password 8ubRu
 login
interface vlan 1
 ip address 10.10.10.100 255.255.255.0
 no shutdown
 exit
do copy running-config startup-config
service password-encryption
banner motd #"Authorized Personnel ONLY!"#
```

Room-146:

```
enable
configure terminal
hostname Room-146
banner motd #"Autorized personnel ONLY!"#
enable password 8ubRu
enable secret C9WrE
line console 0
 password 8ubRu
 login
line vty 0 4
 password 8ubRu
 login
 exit
service password-encryption
interface vlan 1
 ip address 10.10.10.150 255.255.255.0
 no shutdown
 exit
do copy running-config startup-config
```

The PCs, set in Desktop > IP Configuration:

| PC | IP address | Subnet mask |
|---|---|---|
| Manager | 10.10.10.4 | 255.255.255.0 |
| Reception | 10.10.10.5 | 255.255.255.0 |

The configs: [Room-145-running-config.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/lab-05/Room-145-running-config.txt) and [Room-146-startup-config.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/lab-05/Room-146-startup-config.txt).

## Proof it worked

![Check Results, assessment items: 98/98](/assets/img/lab-05/check-results-items.png)

![Check Results, overall feedback](/assets/img/lab-05/check-results-feedback.png)
