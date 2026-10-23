---
layout: post
title: "Lab 6: Build a Switch and Router Network (Packet Tracer)"
tags: [module-11, packet-tracer, cisco-ios, ssh]
---

**Module:** IT533 Module 11, Cisco IOS basics (put-it-together lab)
**Tools:** Cisco Packet Tracer
**Devices:** R1 (ISR4321 router), S1 (2960 switch), PCA and PCB (PCs)
**Time:** 1 hour 32 minutes (Packet Tracer timer)
**Score:** 40/40, 40 of 40 items

## What the lab asked for

Cable a router, a switch and two PCs, then configure everything from the addressing table: PC addressing, then R1 and S1 with a hostname, `class` as the encrypted enable password, `cisco` on the console, encrypted passwords, a warning banner, interface addresses (the SVI and default gateway on the switch) and a save. Part 2 uses `show version`, `show ip route`, `show interfaces` and `show ip interface brief` to answer questions about the gear. Part 3 locks R1's remote access down to SSH only: domain name, RSA keys, a local user, and VTY lines that use it.

## What I connected

| From | To | Cable |
|---|---|---|
| PCA FastEthernet0 | S1 FastEthernet0/1 | Copper straight-through |
| S1 GigabitEthernet0/1 | R1 GigabitEthernet0/0/1 | Copper straight-through |
| R1 GigabitEthernet0/0/0 | PCB FastEthernet0 | Copper straight-through |
| PCA RS 232 | S1 Console | Console (rollover) |
| PCB RS 232 | R1 Console | Console (rollover) |

## What I typed

The commands that ended up in the final configs, cleaned up and in order. The full log, every typo and dead end included, is in [command-log.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/lab-06/command-log.txt).

R1:

```
enable
configure terminal
hostname R1
line console 0
 password cisco
 login
 exit
enable secret class
service password-encryption
banner motd #"Authorized personnel ONLY!"#
interface g0/0/0
 ip address 192.168.0.1 255.255.255.0
 no shutdown
interface g0/0/1
 ip address 192.168.1.1 255.255.255.0
 no shutdown
 exit
line vty 0 4
 password cisco
 login
line vty 5 15
 password cisco
 login
 exit
do copy running-config startup-config
ip domain-name academy.net
crypto key generate rsa
username SSHuser secret cisco
line vty 0 4
 login local
 transport input ssh
```

S1:

```
enable
configure terminal
hostname S1
enable password class
line console 0
 password cisco
 login
line vty 0 15
 password cisco
 login
 exit
banner motd #"Authorized Personnel ONLY!"#
service password-encryption
interface vlan 1
 ip address 192.168.1.2 255.255.255.0
 no shutdown
 exit
ip default-gateway 192.168.1.1
enable secret class
do copy running-config startup-config
```

The PCs:

| PC | IP address | Subnet mask | Default gateway |
|---|---|---|---|
| PCA | 192.168.1.3 | 255.255.255.0 | 192.168.1.1 |
| PCB | 192.168.0.3 | 255.255.255.0 | 192.168.0.1 |

The configs: [R1-running-config.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/lab-06/R1-running-config.txt) and [S1-startup-config.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/lab-06/S1-startup-config.txt).

## The lab's questions

My answers, as I wrote them down during the lab.

**Why were the pings not successful?** Because the computer can’t communicate the switch and the router are not configured.

**Were the pings successful? Explain.** After configuring the router, the ping test was still unsuccessful, and the switch still needs to be configured.

**What is IOS software image and version running on the switch?** Cisco IOS Software, C2960 Software (C2960-LANBASE-M), Version 12.2(25)FX

**What is the model number of the switch?** Cisco WS-C2960-24TT

**What code is used in the routing table to indicate a directly connected network?** C

**How many route entries are coded with a C code in the routing table?** Two route entries.

**What interface types are associated to the C coded routes?** G0/0/0/ and G0/0/1

**What is the operational status of the G0/0/1 interface?** GigabitEthernet0/0/1 is up, line protocol is up (connected).

**What is the Media Access Control (MAC) address of the G0/01 interface?** 0060.3edc.7802 (bia 0060.3edc.7802).

**How is the Internet address displayed in this command?** CIDR 192.168.1.1/24

**If the G0/0/1 interface showed administratively down, what interface configuration command would you use to turn the interface up?** No shutdown command

**What would happen if you had incorrectly configured interface G0/0/1 on the router with an IP address of 192.168.1.2?** PC-A would have not connection to reach the router.

## Proof it worked

![Check Results, assessment items: 40/40](/assets/img/lab-06/check-results-items.png)

![Check Results, overall feedback](/assets/img/lab-06/check-results-feedback.png)
