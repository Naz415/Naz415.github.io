---
layout: post
title: "Lab 2: Basic Device Configuration (Packet Tracer)"
tags: [module-11, packet-tracer, cisco-ios]
---
<!-- Naz: this is a template. Replace every line in [brackets] with your own words, then drop your screenshots into assets/img/lab-02/ and fix the image names. Delete this comment when you're done. -->

**Module:** IT533 Module 11, Cisco IOS basics
**Tools:** Cisco Packet Tracer
**Time:** [about 45 minutes]

## What the lab asked for

[Two or three sentences in your own words. What devices, what the end state was supposed to look like: hostnames, passwords, the management address, the banner, saved config.]

## The addressing table

| Device | Interface | Address | Mask | Gateway |
|---|---|---|---|---|
| [RTA] | [G0/0/0] | [10.10.10.1] | [255.255.255.0] | n/a |
| [SW1] | [Vlan1] | [10.10.10.2] | [255.255.255.0] | [10.10.10.1] |

## What I typed, and why

```
enable
configure terminal
hostname [SW1]
enable secret [class]
line console 0
 password [cisco]
 login
line vty 0 15
 password [cisco]
 login
service password-encryption
banner motd #Authorized access only#
interface vlan 1
 ip address [10.10.10.2 255.255.255.0]
 no shutdown
ip default-gateway [10.10.10.1]
end
copy running-config startup-config
```

[One short paragraph: which of these you did from memory, which one you had to look up, and why the order matters (for example, `login` doing nothing until a password exists).]

## Where I got stuck

[Be specific. The `^` marker you got and what it turned out to mean. A command you ran in the wrong mode. The gateway on the wrong subnet. These paragraphs are the most useful part of the post for the next person.]

## Proof it worked

![Check Results](/assets/img/lab-02/check-results.png)

![show ip interface brief](/assets/img/lab-02/show-ip-int-brief.png)

## What I'd tell someone doing this next

[Three bullets, max.]
