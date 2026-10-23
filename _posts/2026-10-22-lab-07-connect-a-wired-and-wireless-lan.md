---
layout: post
title: "Lab 7: Connect a Wired and Wireless LAN (Packet Tracer)"
tags: [module-11, packet-tracer, cabling]
---

**Module:** IT533 Module 11, Cisco IOS basics
**Tools:** Cisco Packet Tracer
**Devices:** Router0 (1841), Router1 (2621XM), Switch, Cloud, Cable Modem, Wireless Router, Family PC, Home PC, Home Printer, netacad.pka (server), Configuration Terminal
**Time:** 17 minutes (Packet Tracer timer)
**Score:** 80/80, 16 of 16 items

## What the lab asked for

A cabling lab. The devices are already configured; the job is to pick the right cable for every link from the addressing table: copper straight-through to the cloud, coax to the cable modem, serial between the routers, a crossover between Router0 and a server whose NIC can't auto-sense, a console cable for the configuration terminal, and the rest of the home network. Then verify with pings and a web browser, check Router0 from its console, and look at the physical workspace to see how the same network sits in racks and rooms.

## What I connected

| From | To | Cable |
|---|---|---|
| Router0 FastEthernet0/0 | Cloud Ethernet6 | Copper straight-through |
| Cloud Coaxial7 | Cable Modem Port 0 | Coaxial |
| Router0 Serial0/0/0 | Router1 Serial0/0 | Serial |
| Router0 FastEthernet0/1 | netacad.pka FastEthernet0 | Copper cross-over |
| Configuration Terminal RS 232 | Router0 Console | Console (rollover) |
| Router1 FastEthernet1/0 | Switch FastEthernet0/1 | Fiber (multimode) |
| Cable Modem Port 1 | Wireless Router Internet | Copper straight-through |
| Wireless Router Ethernet 1 | Family PC FastEthernet0 | Copper straight-through |

The crossover is the one to remember: Router0 and the server both transmit on pins 1 and 2 and receive on 3 and 6, and neither NIC auto-senses, so a straight-through cable would leave them talking over each other.

## Proof it worked

![Check Results, assessment items: 80/80](/assets/img/lab-07/check-results-items.png)

![Check Results, overall feedback](/assets/img/lab-07/check-results-feedback.png)
