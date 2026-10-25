---
layout: post
title: "Lab 9: Connect the Physical Layer (Packet Tracer)"
tags: [module-12, packet-tracer, cabling]
---

**Module:** IT533 Module 12, the physical layer
**Tools:** Cisco Packet Tracer
**Devices:** East and West (1941 routers), Switch1 and Switch4 (2960 switches), Switch2 and Switch3 (modular PT switches), PC1 to PC9, an access point
**Time:** 53 minutes (Packet Tracer timer)
**Score:** 51/51, 51 of 51 items

## What the lab asked for

Part 1 looks at the East router up close: its management ports, its LAN and WAN interfaces, the default bandwidth on a Gigabit and a serial interface, and the free expansion slots on East and Switch2. Part 2 picks the right modules: one that gives East enough switch ports to connect three PCs directly, and one that gives Switch2 a Gigabit fiber link to Switch3. The modules go in with the power off, because the router's slots aren't hot-swappable. Part 3 cables everything from the lab's table, and Part 4 checks the interface status on East.

## What I added

| Device | Module | Result |
|---|---|---|
| East (powered off first) | HWIC-4ESW | Four switch ports, FastEthernet0/1/0 to 0/1/3, for PC1 to PC3 |
| Switch2, right-most empty slot | PT-SWITCH-NM-1FGE | GigabitEthernet5/1, a fiber port for the link to Switch3 |

## What I connected

| From | To | Cable |
|---|---|---|
| East GigabitEthernet0/0 | Switch1 GigabitEthernet0/1 | Copper straight-through |
| East GigabitEthernet0/1 | Switch4 GigabitEthernet0/1 | Copper straight-through |
| East FastEthernet0/1/0, 0/1/1, 0/1/2 | PC1, PC2, PC3 FastEthernet0 | Copper straight-through |
| Switch1 FastEthernet0/1, 0/2, 0/3 | PC4, PC5, PC6 FastEthernet0 | Copper straight-through |
| Switch4 GigabitEthernet0/2 | Switch3 GigabitEthernet3/1 | Copper cross-over |
| Switch3 GigabitEthernet5/1 | Switch2 GigabitEthernet5/1 | Fiber (multimode) |
| Switch2 FastEthernet0/1, 1/1, 2/1 | PC7, PC8, PC9 FastEthernet0 | Copper straight-through |
| Switch2 GigabitEthernet3/1 | Access point Port 0 | Copper straight-through |
| East Serial0/0/0 (DCE) | West Serial0/0/0 | Serial DCE |

## What I typed

Only show commands; this lab doesn't change any configuration. The full log is in [command-log.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/lab-09/command-log.txt).

```
East> show ip interface brief
East> show interfaces GigabitEthernet0/0
East> show interfaces Serial0/0/0
Switch2> show ip interface brief
```

## The lab's questions

My answers, as I wrote them down during the lab.

**Which management ports are available?** Console and Aux ports.

**Which LAN and WAN interfaces are available on the East router and how many are there?** Ge0/0, Ge0/1, Serial 0, Serial 1

**How many physical interfaces are listed?** 4 physical interfaces 2 serail and 2 Ethernet

**What is the default bandwidth of this interface (Gigabit Ethernet)?** BW 100000 Kbit

**What is the default bandwidth of this interface (Serial)?** BW 1544 Kbit

**How many expansion slots are available to add additional modules to the East router?** 1 expansion slot

**Switch2 - How many expansion slots are available?** 5 expansion slots

**Which module can you use to connect the three PCs to the East router?** The HWIC-4ESW

**How many hosts can you connect to the router using this module?** Provides four switching ports.

**Which module can you insert to provide a Gigabit optical connection to Switch3?** The PT-SWITCH-NM-1FGE Module provides one Gigabit-Ethernet interface for use with multimode mode fiber media. Ideal for a wide range of LAN applications, the Gigabit Ethernet network modules support many internetworking features and standards. Single port network modules offer autosensing 10/100BaseTX or 1000BaseFX Ethernet.

**Into which slot was it inserted?** GigabitEthernet5/1 unassigned YES manual down/down

## Proof it worked

![Check Results, assessment items: 51/51](/assets/img/lab-09/check-results-items.png)

![Check Results, overall feedback](/assets/img/lab-09/check-results-feedback.png)
