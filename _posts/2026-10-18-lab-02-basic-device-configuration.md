---
layout: post
title: "Lab 2: Basic Device Configuration (Packet Tracer)"
tags: [module-11, packet-tracer, cisco-ios, ipv6]
---
<!-- Naz: the topology, requirements and addressing below come from the lab file (Lab 2-Packet Tracer - Basic Device Configuration.pka). The lab hands out one of three name and address sets at random; this post uses the set stored in the file (RTA, ASw-1, ASw-2, 10.10.10.0/24 and 10.10.11.0/24). If your Check Results showed different names (College/Class-A or Floor14/Room-145), swap them in. The commands are what the lab requires; change them to what you actually typed. Replace every line in [brackets] with your own words, then drop your screenshots into assets/img/lab-02/. Delete this comment when you're done. -->

**Module:** IT533 Module 11, Cisco IOS basics
**Tools:** Cisco Packet Tracer
**Devices:** RTA (1941 router), ASw-1 and ASw-2 (3650 switches), User-01 to User-04 (PCs)
**Time:** [about 45 minutes]

## What the lab asked for

[Two or three sentences in your own words. One router joining two LANs. Configure the router and the second switch (ASw-1 is locked), finish the hosts' IPv4 and IPv6 settings, fill in the missing parts of the addressing table, then get every device pinging every other device over IPv4 and IPv6.]

The requirements list: name the devices, `cisco` on all lines, `class` as the encrypted enable password, encrypt plaintext passwords, a banner, IPv4 and IPv6 on RTA and ASw-2, descriptions on interfaces (including ASw-2's VLAN 1), save, then verify and troubleshoot.

## The addressing table

| Device | Interface | IPv4 / IPv6 | Default gateway |
|---|---|---|---|
| RTA | G0/0 | 10.10.10.1/24 | n/a |
| RTA | G0/0 | 2001:DB8:ACAD:100::1/64 | n/a |
| RTA | G0/0 | FE80::2 link-local | n/a |
| RTA | G0/1 | 10.10.11.1/24 | n/a |
| RTA | G0/1 | 2001:DB8:ACAD:200::1/64 | n/a |
| RTA | G0/1 | FE80::3 link-local | n/a |
| ASw-1 | VLAN 1 | 10.10.10.100/24 | [ ] |
| ASw-2 | VLAN 1 | 10.10.11.100/24 | [ ] |
| User-01 | NIC | 10.10.10.101/24, 2001:DB8:ACAD:100::50/64 | [ ] |
| User-02 | NIC | 10.10.10.102/24, 2001:DB8:ACAD:100::60/64 | [ ] |
| User-03 | NIC | 10.10.11.101/24, 2001:DB8:ACAD:200::50/64 | [ ] |
| User-04 | NIC | 10.10.11.102/24, 2001:DB8:ACAD:200::60/64 | [ ] |

[Fill in the gateway column. That's part of the lab's "complete the documentation" step.]

## What I typed, and why

On the router:

```
enable
configure terminal
hostname RTA
enable secret class
line console 0
 password cisco
 login
line vty 0 15
 password cisco
 login
service password-encryption
banner motd #Authorized access only#
ipv6 unicast-routing
interface g0/0
 description LAN connection to ASw-1
 ip address 10.10.10.1 255.255.255.0
 ipv6 address 2001:db8:acad:100::1/64
 ipv6 address fe80::2 link-local
 no shutdown
interface g0/1
 description LAN connection to ASw-2
 ip address 10.10.11.1 255.255.255.0
 ipv6 address 2001:db8:acad:200::1/64
 ipv6 address fe80::3 link-local
 no shutdown
end
copy running-config startup-config
```

On ASw-2:

```
enable
configure terminal
hostname ASw-2
enable secret class
line console 0
 password cisco
 login
line vty 0 15
 password cisco
 login
service password-encryption
banner motd #Authorized access only#
interface vlan 1
 description Connection to RTA
 ip address 10.10.11.100 255.255.255.0
 ipv6 address 2001:db8:acad:200::100/64
 no shutdown
exit
ip default-gateway 10.10.11.1
end
copy running-config startup-config
```

On each PC: Desktop > IP Configuration, finish the IPv4 settings and enter the IPv6 address, prefix length and gateway.

[One short paragraph: which of these you did from memory, which one you had to look up, and why `ipv6 unicast-routing` matters for the PCs on one LAN reaching the other.]

## Where I got stuck

[Be specific. The lab plants at least one problem for you to find: not every host starts out in the right place. Which device couldn't ping, what did `ipconfig` show, and what did you change? Also: the `^` marker you got, or a command you ran in the wrong mode.]

## Proof it worked

![Check Results](/assets/img/lab-02/check-results.png)

![show ip interface brief](/assets/img/lab-02/show-ip-int-brief.png)

## What I'd tell someone doing this next

[Three bullets, max.]
