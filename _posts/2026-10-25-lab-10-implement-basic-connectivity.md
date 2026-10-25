---
layout: post
title: "Lab 10: Implement Basic Connectivity (Packet Tracer)"
tags: [module-12, packet-tracer, cisco-ios]
---

**Module:** IT533 Module 12, basic connectivity
**Tools:** Cisco Packet Tracer
**Devices:** S1 and S2 (2960 switches), PC1 and PC2
**Time:** 46 minutes (Packet Tracer timer)
**Score:** 88/88, 22 of 22 items

## What the lab asked for

Give two switches a basic configuration: a hostname, `cisco` on the console, `class` as the encrypted privileged EXEC password, a warning banner, and a save to NVRAM. Then address the PCs from the addressing table and try to ping S1 before the switch has an IP address. Last, give each switch a management IP on VLAN 1, bring the interface up, save, and ping between every device.

## What I typed

The commands that ended up in the final configs, cleaned up and in order. The full log, every typo and dead end included, is in [command-log.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/lab-10/command-log.txt).

S1:

```
enable
configure terminal
hostname S1
line console 0
 password cisco
 login
 exit
banner motd #"Authorized access only. Violators will be prosecuted to the full extent of the law."#
interface vlan 1
 ip address 192.168.1.253 255.255.255.0
 no shutdown
 exit
service password-encryption
line vty 0 15
 password cisco
 login
 exit
no enable password
enable secret class
end
copy running-config startup-config
```

S2:

```
enable
configure terminal
hostname S2
line console 0
 password cisco
 login
 exit
banner motd #"Authorized access only. Violators will be prosecuted to the full extent of the law."#
interface vlan 1
 ip address 192.168.1.254 255.255.255.0
 no shutdown
 exit
service password-encryption
line vty 0 15
 password cisco
 login
 exit
no enable password
enable secret class
end
copy running-config startup-config
```

The first time, I set the privileged password with `enable password class`. When I added `enable secret class`, IOS refused it because it matched the existing enable password, so I removed the old one with `no enable password` and set the secret again.

The PCs:

| PC | IP address | Subnet mask |
|---|---|---|
| PC1 | 192.168.1.1 | 255.255.255.0 |
| PC2 | 192.168.1.2 | 255.255.255.0 |

The configs: [S1-startup-config.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/lab-10/S1-startup-config.txt) and [S2-startup-config.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/lab-10/S2-startup-config.txt).

## The lab's questions

My answers, as I wrote them down during the lab.

**How can you verify that both passwords were configured correctly?** With command show running-config.

**Which command do you issue to accomplish this step?** copy run start

**Were you successful? Explain.** No, the ping test failed. Reviewing the running config on both switches there is no interface assigned with that IP address.

**If this is the case, why would we configure it with an IP address?** We give the switch an IP address on VLAN 1 to be able to ping or test connectivity and to be able to remote into the switch from any pc on the network. Applying the line vty 0 15 password allows for an Telnet connection to the switch.

**Why do you enter the no shutdown command?** The command enables the interface from a down state to an up state.

**Which command is used to save the configuration file in RAM to NVRAM?** copy run start

## Proof it worked

![Check Results, assessment items: 88/88](/assets/img/lab-10/check-results-items.png)

![Check Results, overall feedback](/assets/img/lab-10/check-results-feedback.png)
