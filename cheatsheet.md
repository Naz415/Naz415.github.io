---
layout: page
title: Cisco IOS cheat sheet
permalink: /cheatsheet/
---
The commands every IT533 Packet Tracer lab in Module 11 uses, in the order you type them. Prompts show which mode you need to be in.

## The mode ladder

| Prompt | Mode | Get there with |
|---|---|---|
| `Switch>` | User EXEC | where you start |
| `Switch#` | Privileged EXEC | `enable` |
| `Switch(config)#` | Global config | `configure terminal` |
| `Switch(config-if)#` | Interface config | `interface vlan 1` |
| `Switch(config-line)#` | Line config | `line console 0` |

`exit` goes back one level. `end` (or Ctrl+Z) goes straight to `#`. `do show run` runs a `#` command from inside config mode.

## Identity and passwords (global config)

```
hostname S1
banner motd #Authorized access only#
enable secret class
line console 0
 password cisco
 login
line vty 0 15
 password cisco
 login
service password-encryption
```

`enable secret` is hashed and wins over `enable password`. `login` is what turns a line password on. `service password-encryption` is type 7: it hides, it doesn't protect.

## Switch management address

```
interface vlan 1
 ip address 10.10.20.2 255.255.255.0
 no shutdown
exit
ip default-gateway 10.10.20.1
```

Vlan1 starts administratively down. The gateway is global, takes no mask, and must be on the same subnet as the switch.

## Router interface

```
interface g0/0/0
 description Link to S1
 ip address 10.10.20.1 255.255.255.0
 no shutdown
```

Router ports start shut down; switch ports start up. Routers don't use `ip default-gateway`.

## Check and save

```
show ip interface brief
show running-config
copy running-config startup-config
show startup-config
reload
```

`show ip interface brief` is the one-line table (Status / Protocol). `show interfaces` is the long report. "startup-config is not present" means you never saved.

## The errors

| Message | Means |
|---|---|
| `% Invalid input detected at '^' marker.` | wrong mode, or a typo at the `^` |
| `% Incomplete command.` | the command needs more words |
| `% Ambiguous command:` | your abbreviation matches more than one command |
| `% Bad secrets` | wrong enable secret three times |
