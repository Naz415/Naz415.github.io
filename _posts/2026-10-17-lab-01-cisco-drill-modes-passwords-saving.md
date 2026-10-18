---
layout: post
title: "Lab 1: Cisco Drill 1, Modes, Passwords, Banner, Interfaces, Saving (Packet Tracer)"
tags: [module-11, packet-tracer, cisco-ios]
---
<!-- Naz: the commands, addressing table and config links below come from your saved drill-01 configs. Replace every line in [brackets] with your own words, then drop your screenshots into assets/img/lab-01/ and fix the image names. Delete this comment when you're done. -->

**Module:** IT533 Module 11, Cisco IOS basics
**Tools:** Cisco Packet Tracer
**Devices:** S1 (Catalyst 2960), R1 (ISR4221)
**Time:** [about 45 minutes]

## What the lab asked for

[Two or three sentences in your own words. Two devices, one link. Name them, lock the console, VTY and privileged mode, put up a banner, give the switch a management address and the router its interface address, then save so it all survives a reload.]

## The addressing table

| Device | Interface | Address | Mask | Gateway |
|---|---|---|---|---|
| R1-LAB1 | G0/0/0 | 10.10.20.1 | 255.255.255.0 | n/a |
| S1-LAB1 | Vlan1 | 10.10.20.2 | 255.255.255.0 | 10.10.20.1 |

## What I typed, and why

On the switch:

```
enable
configure terminal
hostname S1-LAB1
enable secret class
line console 0
 password cisco
 login
line vty 0 15
 password cisco
 login
service password-encryption
banner motd #Authorized access only. Violaters will be prosecuted.#
interface vlan 1
 ip address 10.10.20.2 255.255.255.0
 no shutdown
exit
ip default-gateway 10.10.20.1
end
copy running-config startup-config
```

On the router:

```
enable
configure terminal
hostname R1-LAB1
enable secret class
line console 0
 password cisco
 login
line vty 0 4
 password cisco
 login
interface g0/0/0
 description #Link to S1.#
 ip address 10.10.20.1 255.255.255.0
 no shutdown
end
copy running-config startup-config
```

[One short paragraph: which of these you did from memory, which one you had to look up, and why the order matters. For example, the switch's Vlan1 and the router's G0/0/0 both start down, so nothing pings until `no shutdown`.]

The saved configs are in the repo: [S1-startup-config.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/drill-01/S1-startup-config.txt) and [R1-startup-config.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/drill-01/R1-startup-config.txt).

## Where I got stuck

[Be specific. A few things your saved configs show that are worth a sentence each, if they were part of it:]

- [The router's description saved as `#Link to S1.#`. A description takes the rest of the line as plain text, so the `#` marks are kept. Only `banner` uses a delimiter. Did you carry that habit over from the banner?]
- [S1 has `service password-encryption` and R1 doesn't, so R1's console and VTY passwords show as plain `cisco` in its config. Was that on purpose or a step you skipped?]
- [R1 has no banner. Did the lab ask for one on the router?]
- [The `^` marker you got and what it turned out to mean, or a command you ran in the wrong mode.]

## Proof it worked

![Check Results](/assets/img/lab-01/check-results.png)

![show ip interface brief](/assets/img/lab-01/show-ip-int-brief.png)

## What I'd tell someone doing this next

[Three bullets, max.]
