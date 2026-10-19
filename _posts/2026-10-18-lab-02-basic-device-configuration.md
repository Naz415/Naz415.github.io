---
layout: post
title: "Lab 2: Basic Device Configuration (Packet Tracer)"
tags: [module-11, packet-tracer, cisco-ios, ipv6]
---
<!-- Naz: the device names, addressing table, commands and screenshots come from your saved lab (Documents\IT533 Labs\Lab 2 ...\Lab 2-Packet Tracer - Basic Device Configuration.pka) and your Word write-up, worked Oct 18. Your name is blacked out of the screenshots. Replace every line in [brackets] with your own words. Delete this comment when you're done. -->

**Module:** IT533 Module 11, Cisco IOS basics
**Tools:** Cisco Packet Tracer
**Devices:** Floor14 (1941 router), Room-145 and Room-146 (3650 switches), Manager-A, Reception-A, Manager-B, Reception-B (PCs)
**Time:** 1 hour 35 minutes (Packet Tracer timer)
**Score:** 134/134, 44 of 44 items

## What the lab asked for

[Two or three sentences in your own words. One router joining two LANs. Configure the router and Room-146 (Room-145 is locked), finish the PCs' IPv4 and IPv6 settings, fill in the addressing table, then get every device pinging every other device over IPv4 and IPv6.]

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
| Room-145 | VLAN 1 | 10.10.10.100/24 | 10.10.10.1/24 |
| Room-146 | VLAN 1 | 10.10.11.100/24 | 10.10.11.1/24 |
| Manager-A | NIC | 10.10.10.101/24 | 10.10.10.1/24 |
| Manager-A | NIC | 2001:DB8:ACAD:100::50/64 | 2001:DB8:ACAD:100::1/64 |
| Reception-A | NIC | 10.10.10.102/24 | 10.10.10.1/24 |
| Reception-A | NIC | 2001:DB8:ACAD:100::60/64 | 2001:DB8:ACAD:100::1/64 |
| Manager-B | NIC | 10.10.11.101/24 | 10.10.11.1/24 |
| Manager-B | NIC | 2001:DB8:ACAD:200::50/64 | 2001:DB8:ACAD:200::1/64 |
| Reception-B | NIC | 10.10.11.102/24 | 10.10.11.1/24 |
| Reception-B | NIC | 2001:DB8:ACAD:200::60/64 | 2001:DB8:ACAD:200::1/64 |

## What I typed, and why

These are the commands that ended up in the saved configs, cleaned up and in order. The full log, every typo included, is in [command-log.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/lab-02/command-log.txt).

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
 description #Link to Room-146 Switch#
 ip address 10.10.10.1 255.255.255.0
 ipv6 address 2001:db8:acad:100::1/64
 ipv6 address fe80::2 link-local
 no shutdown
interface g0/1
 description #Link to Room-145 switch.#
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
 description #Link to Floor14 G0/0.#
 ip address 10.10.11.100 255.255.255.0
 ipv6 address 2001:DB8:ACAD:100::1/64
 no shutdown
exit
ip default-gateway 10.10.10.1
do copy running-config startup-config
```

On each PC: Desktop > IP Configuration, static IPv4 and IPv6, with the IPv6 gateway set to the router's link-local address (FE80::2 on the G0/0 side, FE80::3 on the G0/1 side).

The saved configs: [Floor14-startup-config.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/lab-02/Floor14-startup-config.txt) and [Room-146-startup-config.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/lab-02/Room-146-startup-config.txt).

[One short paragraph: which of these you did from memory, which one you had to look up, and why `ipv6 unicast-routing` matters for the PCs on one LAN reaching the other.]

## Where I got stuck

[Be specific. A few moments the log shows, if they were part of it:]

- [`hostname Floor 14` with a space, typed at `Router>` and `Router#` before I got it into config mode. What does each prompt allow?]
- [`motd banner` instead of `banner motd`, three times, before it took.]
- [`int g0/0/0` didn't work on the 1941. Its ports are `g0/0` and `g0/1`. Where did the extra `/0` come from?]
- [`ip default-gateway 10.10.10.1 255.255.255.0`: the gateway doesn't take a mask.]
- [`copy running-config startup-config` at `(config)#` failed, `do copy ...` worked. Same for `show` commands: `run` isn't an IOS command, `do` is.]
- [`ipv6 route ::/0 vlan 1 fe80::3` went on the router, pointing at its own shut-down Vlan1 and its own G0/1 link-local. Does a router need that line?]
- [Reception-B started out with the wrong address. That was the troubleshooting item. How did I spot it?]

## Proof it worked

![Check Results, assessment items: 134/134](/assets/img/lab-02/check-results-items.png)

![Check Results, overall feedback](/assets/img/lab-02/check-results-feedback.png)

## What I'd tell someone doing this next

[Three bullets, max.]
