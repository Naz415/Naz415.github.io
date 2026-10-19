---
layout: post
title: "Lab 1: Navigate the IOS (Packet Tracer)"
tags: [module-11, packet-tracer, cisco-ios]
---

**Module:** IT533 Module 11, Cisco IOS basics
**Tools:** Cisco Packet Tracer
**Devices:** PC1, S1 (Catalyst 2960-24TT)
**Time:** 1 hour 10 minutes (Packet Tracer timer)

## What the lab asked for

Three parts: connect PC1 to S1 with a console cable and explore the IOS help, move between user EXEC, privileged EXEC and global configuration mode, then use the `clock` command to practice command syntax and error messages.

## The setup

No IP addressing in this one. It's one cable:

| From | Port | To | Port | Cable |
|---|---|---|---|---|
| PC1 | RS 232 | S1 | Console | Console (light blue) |

Then PC1 > Desktop > Terminal, keep the default port settings, and press Enter at "Press RETURN to get started!"

## What I typed

This is my actual command log from the lab, in order:

```
S1> ?
S1> t?
S1> tte?
S1> te?
S1> te
S1> ?
S1> enable
S1# ?
S1# c?
S1# configure
S1(config)# exit
S1# config
S1(config)# exit
S1# show clock
S1# clock
S1# clock?
S1# clock set?
S1> enable
S1# clock set 15:00:00 ?
S1# clock set 15:00:00 01/31/2035
S1# clock set 15:00:00 January 31 2035 ?
S1# clock set 15:00:00 January 31 2035
S1# show clock
S1# cl<Tab>
S1# ock
S1# clock
S1# clock set 25:00:00
S1# clock set 15:00:00 32
S1# exit
```

## The lab's questions

My answers, as I wrote them down during the lab.

**What is the setting for bits per second?** 9600

**What is the prompt displayed on the screen?** The prompt displayed on the screen is Press RETURN to get started! After pressing RETURN, we see terminal line 1 labeled S1>.

**Which commands are displayed?** Typing "?" I get a list of EXEC commands. Typing "t?" I get all commands starting with the letter "t". Typing "te?" I get a list of commands that start with "te".

**What information is displayed for the enable command?** It states that "enable" turns on privileged commands.

**What displays after pressing the Tab key?** The "enable" command is autofill.

**What would happen if you typed `te<Tab>` at the prompt?** It would tab complete "telnet".

**How does the prompt change?** It changes from S1> to S1#.

**How many commands are displayed now that privileged EXEC mode is active?** Typing "?" we see about 20+ commands, typing "c?" I see about 5 commands.

**What is the message that is displayed?** "Configuring from terminal, memory, or network [terminal]?" After pressing "ENTER," Enter configuration commands, one per line. End with CNTL/Z.

**What information is displayed for `show clock`? What is the year that is displayed?** Time is displayed in UTC time. The year is 1993.

**What information is displayed for `clock`?** % Incomplete command.

**What information is displayed for `clock ?`** "clock"

**What information is being requested by `clock set ?`** The time to be set is being requested.

**What would have been displayed if only the clock set command had been entered, and no request for help was made by using the question mark?** % Incomplete command.

### The error messages

| Command | What was returned |
|---|---|
| `S1# cl<Tab>` | No command completion. No output. |
| `S1# clock` | % Incomplete command. |
| `S1# clock set 25:00:00` | % Invalid input detected at '^' marker. |
| `S1# clock set 15:00:00 32` | % Invalid input detected at '^' marker. |

## Proof it worked

Packet Tracer marked the activity complete, time elapsed 1:10:50.

![Check Results, overall feedback](/assets/img/lab-01/check-results-feedback.png)

![Check Results, assessment items](/assets/img/lab-01/check-results-items.png)
