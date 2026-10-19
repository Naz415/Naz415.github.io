---
layout: post
title: "Lab 3: Configure Initial Switch Settings (Packet Tracer)"
tags: [module-11, packet-tracer, cisco-ios]
---

**Module:** IT533 Module 11, Cisco IOS basics
**Tools:** Cisco Packet Tracer
**Devices:** S1, S2 (Catalyst 2960-24TT), PC1, PC2
**Time:** 10 minutes (Packet Tracer timer)
**Score:** 72/72, 16 of 16 items

## What the lab asked for

Five parts: check the default switch configuration, give S1 a name and secure its console and privileged mode with plain, secret and encrypted passwords, add a MOTD banner, save to NVRAM, then configure S2 the same way without step-by-step instructions.

The lab's passwords: `letmein` on the console, `c1$c0` as the enable password, `itsasecret` as the enable secret.

## What I typed

On S1:

```
enable
configure terminal
hostname S1
line console 0
 password letmein
 login
 exit
enable password c1$c0
enable secret itsasecret
service password-encryption
banner motd "This is a secure system. Authorized Access Only!"
exit
copy running-config startup-config
```

On S2:

```
enable
configure terminal
line console 0
 password letmein
 login
 exit
enable password c1$c0
enable secret itsasecret
service password-encryption
banner motd "This is a secure system. Authorized Access Only!"
hostname S2
exit
copy running-config startup-config
```

The full log, typos included, is in [command-log.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/lab-03/command-log.txt). The saved configs: [S1-startup-config.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/lab-03/S1-startup-config.txt) and [S2-startup-config.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/lab-03/S2-startup-config.txt).

## The lab's questions

My answers, as I wrote them down during the lab.

**How many Fast Ethernet interfaces does the switch have?** After running the show running-config command, I can see the switch has 24 Fast Ethernet interaces.

**How many Gigabit Ethernet interfaces does the switch have?** After running the show running-config command, I can see the switch has 2 Gigabit Ethernet interfaces.

**What is the range of values shown for the vty lines?** The range for vty lines is 0-4 and 5-15.

**Which command will display the current contents of non-volatile random-access memory (NVRAM)?** The show running-config command

**Why does the switch respond with "startup-config is not present"?** There is nothing saved to the nvram memory.

**Why is the login command required?** The login command is required to enable the password when logging in to the router or switch.

**What is displayed for the enable secret password?** $1$mERr$ILwq/b7kc.7X/ejA4Aosn0

**Why is the enable secret password displayed differently from what we configured?** The password is seen as a type 5 MD5 hash.

**If you configure any more passwords on the switch, will they be displayed in the configuration file as plain text or in encrypted form? Explain.** If I configure more passwords on the switch they will be encrypted and be hidden from plain sight. Enabling the password encryption hides all passwords that show in plain text.

**When will this banner be displayed?** The banner will be displayed at next login.

**Why should every switch have a MOTD banner?** To notify unauthorized users that they should not have accessed the device it is a warning, not an invitation.

**What is the shortest, abbreviated version of the copy running-config startup-config command?** Write memory

**Examine the startup configuration file. Which command will display the contents of NVRAM?** show running-config

**Are all the changes that were entered recorded in the file?** Yes, all changes made show here.

## Proof it worked

![Check Results, assessment items: 72/72](/assets/img/lab-03/check-results-items.png)

![Check Results, overall feedback](/assets/img/lab-03/check-results-feedback.png)
