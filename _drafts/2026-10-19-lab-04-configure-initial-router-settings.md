---
layout: post
title: "Lab 4: Configure Initial Router Settings (Packet Tracer)"
tags: [module-11, packet-tracer, cisco-ios]
---

**Module:** IT533 Module 11, Cisco IOS basics
**Tools:** Cisco Packet Tracer
**Devices:** R1 (1941 router), PCA (console connection)
**Time:** about an hour (15:10 to 16:08 in the command log)

## What the lab asked for

Look over R1's default configuration, then set it up: name it R1, add a MOTD banner, and lock it down with three passwords (privileged EXEC unencrypted `cisco`, privileged EXEC encrypted `itsasecret`, console `letmein`), encrypt the plain-text ones, save to NVRAM, and look at what's stored in flash.

## What I typed

The commands that ended up in R1's final config, cleaned up and in order. The full log, every typo and wrong-mode command included, is in [command-log.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/lab-04/command-log.txt).

```
enable
configure terminal
hostname R1
banner motd #"Unauthorized access is strictly prohibited."#
line console 0
 password letmein
 login
line vty 0 4
 password cisco
 login
 exit
service password-encryption
enable password cisco
enable secret itsasecret
end
copy running-config startup-config
show flash
```

The final config: [R1-running-config.txt](https://github.com/Naz415/Naz415.github.io/blob/main/configs/lab-04/R1-running-config.txt).

## Where I got stuck

[In your own words. Your command log shows the story: what happened when `enable password letmein` was typed at the `(config-line)#` prompt, what `enable secret itsasecret` did when typed at `R1#`, and why Check Results marked Enable Password wrong until 15:45.]

## The lab's questions

My answers, as I wrote them down during the lab.

**What is the router's hostname?** Router

**How many Fast Ethernet interfaces does the router have?** 4 Fast Ethernet ports

**How many Gigabit Ethernet interfaces does the router have?** 2 gigabit ports

**How many Serial interfaces does the router have?** 2 Serial ports

**What is the range of values shown for the vty lines?** The range is 0-4.

**Why does the router respond with the startup-config is not present message?** Because currently the running config is not saved to the NVRAM.

**Why should every router have a message-of-the-day (MOTD) banner?** A warning to keep unauthorized users out. Not an invitation.

**Why would the enable secret password allow access to the privileged EXEC mode and the enable password no longer be valid?** Because the enable secret takes precedence over the enable password as it is MD5 hashed; no more plain text password.

**If you configure any more passwords on the router, are they displayed in the configuration file as plain text or in encrypted form? Explain.** Any other passwords would be encrypted and we enabled secret password, which encrypts all passwords.

**What command did you enter to save the configuration to NVRAM?** Copy running-config startup-config

**What is the shortest, unambiguous version of this command?** Write memory

**How many files are currently stored in flash?** There are 3 files stored in flash.

**Which of these files would you guess is the IOS image?** File number 3: c1900-universalk9-mz.SPA.151-4.M4.bin

**Why do you think this file is the IOS image?** This is the .bin file; all other files are XML.

## Proof it worked

![Check Results, assessment items](/assets/img/lab-04/check-results-items.png)

![Check Results, overall feedback](/assets/img/lab-04/check-results-feedback.png)
