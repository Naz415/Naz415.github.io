---
layout: post
title: "Lab 2: Basic Device Configuration (Packet Tracer)"
tags: [module-11, packet-tracer, cisco-ios, ipv6]
---

**Module:** IT533 Module 11, Cisco IOS basics
**Tools:** Cisco Packet Tracer
**Devices:** Floor14 (1941 router), Room-145 and Room-146 (3650 switches), Manager-A, Reception-A, Manager-B, Reception-B (PCs)
**Time:** 1 hour 35 minutes (Packet Tracer timer)
**Score:** 134/134, 44 of 44 items

## What the lab asked for

One router joining two LANs. Configure the router and the second switch (the first switch is locked), finish the PCs' IPv4 and IPv6 settings, complete the addressing table, then get every device pinging every other device over IPv4 and IPv6. The requirements: name the devices, `cisco` on all lines, `class` as the encrypted enable password, encrypt plaintext passwords, a banner, IPv4 and IPv6 addressing, interface descriptions, save, then verify and troubleshoot.

The lab hands out one of three name and address sets at random. Mine was Floor14 / Room-145 / Room-146 on 10.10.10.0/24 and 10.10.11.0/24.

## The addressing table

My completed table:

| Device | Interface | IP Address | Default Gateway |
|---|---|---|---|
| Floor14 | G0/0 | 10.10.10.1/24 | N/A |
| Floor14 | G0/0 | 2001:DB8:ACAD:100::1/64 | N/A |
| Floor14 | G0/0 | FE80::2 | N/A |
| Floor14 | G0/1 | 10.10.11.1/24 | N/A |
| Floor14 | G0/1 | 2001:DB8:ACAD:200::1/64 | N/A |
| Floor14 | G0/1 | FE80::3 | N/A |
| Room-145 | VLAN 1 | 10.10.10.100/24 | 10.10.10.1 |
| Room-146 | VLAN 1 | 10.10.11.100/24 | 10.10.11.1 |
| Manager-A | NIC | 10.10.10.101/24 | 10.10.10.1 |
| Manager-A | NIC | 2001:DB8:ACAD:100::50/64 | FE80::2 |
| Reception-A | NIC | 10.10.10.102/24 | 10.10.10.1 |
| Reception-A | NIC | 2001:DB8:ACAD:100::60/64 | FE80::2 |
| Manager-B | NIC | 10.10.11.101/24 | 10.10.11.1 |
| Manager-B | NIC | 2001:DB8:ACAD:200::50/64 | FE80::3 |
| Reception-B | NIC | 10.10.11.102/24 | 10.10.11.1 |
| Reception-B | NIC | 2001:DB8:ACAD:200::60/64 | FE80::3 |

## What I typed

These are the commands that ended up in the saved configs, cleaned up and in order, including the fixes from my second pass. The full log, every typo included, is in [command-log.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/lab-02/command-log.txt).

On the router:

```
enable
configure terminal
hostname Floor14
enable secret class
banner motd #Authorized access only. Violators will be prosecuted.#
line console 0
 password cisco
 login
line vty 0 15
 password cisco
 login
service password-encryption
ipv6 unicast-routing
ipv6 route ::/0 vlan 1 fe80::3
interface g0/0
 description Link to Room-145
 ip address 10.10.10.1 255.255.255.0
 ipv6 address 2001:db8:acad:100::1/64
 ipv6 address fe80::2 link-local
 no shutdown
interface g0/1
 description Link to Room-146
 ip address 10.10.11.1 255.255.255.0
 ipv6 address 2001:db8:acad:200::1/64
 ipv6 address fe80::3 link-local
 no shutdown
end
copy running-config startup-config
```

On Room-146:

```
enable
configure terminal
hostname Room-146
enable secret class
banner motd #Authorized access only. Violators will be prosecuted.#
line console 0
 password cisco
 login
line vty 0 15
 password cisco
 login
service password-encryption
interface vlan 1
 description Link to Floor14 G0/1
 ip address 10.10.11.100 255.255.255.0
 ipv6 address 2001:DB8:ACAD:200::100/64
 no shutdown
exit
ip default-gateway 10.10.11.1
do copy running-config startup-config
```

On each PC: Desktop > IP Configuration, static IPv4 and IPv6, with the IPv6 gateway set to the router's link-local address (FE80::2 on the G0/0 side, FE80::3 on the G0/1 side).

The saved configs: [Floor14-startup-config.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/lab-02/Floor14-startup-config.txt) and [Room-146-startup-config.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/lab-02/Room-146-startup-config.txt).

## Second pass (Oct 19)

Check Results was already 134/134, but going back over the configs turned up four things the grader didn't check:

- Room-146's default gateway was 10.10.10.1, the router's address on the other LAN. Changed to 10.10.11.1.
- Room-146's VLAN 1 IPv6 address was 2001:DB8:ACAD:100::1, which is Floor14's G0/0 address. Changed to 2001:DB8:ACAD:200::100/64.
- The router's two interface descriptions were swapped, and Room-146's pointed at G0/0 instead of G0/1.
- My addressing table listed the PCs' IPv6 gateways as the global ::1 addresses. The PCs actually use the router's link-local addresses, FE80::2 and FE80::3.

## Proof it worked

![Check Results, assessment items: 134/134](/assets/img/lab-02/check-results-items.png)

![Check Results, overall feedback](/assets/img/lab-02/check-results-feedback.png)
