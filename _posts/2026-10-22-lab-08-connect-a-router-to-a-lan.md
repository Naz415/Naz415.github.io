---
layout: post
title: "Lab 8: Connect a Router to a LAN (Packet Tracer)"
tags: [module-11, packet-tracer, cisco-ios]
---

**Module:** IT533 Module 11, Cisco IOS basics
**Tools:** Cisco Packet Tracer
**Devices:** R1 and R2 (1941 routers), S1 to S4 (2960 switches, preconfigured), PC1 to PC4
**Time:** 56 minutes (Packet Tracer timer)
**Score:** 54/54, 18 of 18 items

## What the lab asked for

Two partly configured routers joined by a serial link, each with two LANs. Part 1 uses `show interfaces`, `show ip interface brief` and `show ip route` to read the routers' current state. Part 2 addresses, describes and activates the Gigabit Ethernet interfaces on both routers from the addressing table, then saves to NVRAM. Part 3 verifies with the same show commands and end-to-end pings.

## What I typed

The commands that ended up in the final configs, cleaned up and in order. The full log, including every show command I ran for the questions, is in [command-log.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/lab-08/command-log.txt).

R1:

```
enable
configure terminal
interface g0/0
 ip address 192.168.10.1 255.255.255.0
 no shutdown
 description LAN connection to S1
interface g0/1
 ip address 192.168.11.1 255.255.255.0
 no shutdown
 description LAN connection to S2
interface s0/0/0
 ip address 209.165.200.226 255.255.255.252
 no shutdown
 description Serial (DCE) connection to R2
 end
copy running-config startup-config
```

R2:

```
enable
configure terminal
interface g0/0
 ip address 10.1.1.1 255.255.255.0
 no shutdown
 description LAN connection to S3
interface g0/1
 ip address 10.1.2.1 255.255.255.0
 no shutdown
 description LAN connection to S4
interface s0/0/0
 ip address 209.165.200.226 255.255.255.252
 no shutdown
 end
copy running-config startup-config
```

The saved configs: [R1-startup-config.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/lab-08/R1-startup-config.txt) and [R2-startup-config.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/lab-08/R2-startup-config.txt).

## The lab's questions

My answers, as I wrote them down during the lab.

**Which command displays the statistics for all interfaces configured on a router?** show interfaces

**Which command displays the information about the Serial 0/0/0 interface only?** show interfaces serial 0/0/0

**What is the IP address configured on R1?** 209.165.200.225/30

**What is the bandwidth on the Serial 0/0/0 interface?** BW 1544 Kbit

**What is the IP address on R1?** No IP address

**What is the MAC address of the GigabitEthernet 0/0 interface?** 000d.bd6c.7d01 (bia 000d.bd6c.7d01)

**What is the bandwidth (BW) of the GigabitEthernet 0/0 interface?** BW 100000 Kbit

**Which command displays a brief summary of the current interfaces, interface status, and the IP addresses assigned to them?** Show ip int brief

**How many serial interfaces are there on R1 and R2?** 2 serial interfaces each s0/0/0 & s0/0/1.

**How many Ethernet interfaces are there on R1 and R2?** 4 Fast Ethernet ports on R1 only, R2 has no Fast Ethernet ports.

**Are all the Ethernet interfaces on R1 the same? If no, explain the difference(s).** Yes all Ethernet interfaces are the same.

## Proof it worked

![Check Results, assessment items: 54/54](/assets/img/lab-08/check-results-items.png)

![Check Results, overall feedback](/assets/img/lab-08/check-results-feedback.png)
