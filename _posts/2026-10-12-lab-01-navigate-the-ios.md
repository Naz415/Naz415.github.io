---
layout: post
title: "Lab 1: Navigate the IOS (Packet Tracer)"
tags: [module-11, packet-tracer, cisco-ios]
---
<!-- Naz: the setup, the command log and the lab's questions below come straight from your saved Packet Tracer file (Lab 1-Packet Tracer - Navigate the IOS (1).pka, worked Oct 12). Replace every line in [brackets] with your own words, then drop your screenshots into assets/img/lab-01/ and fix the image names. Delete this comment when you're done. -->

**Module:** IT533 Module 11, Cisco IOS basics
**Tools:** Cisco Packet Tracer
**Devices:** PC1, S1 (Catalyst 2960-24TT)
**Time:** about an hour (11:00 to 12:00 by the command log)

## What the lab asked for

[Two or three sentences in your own words. Console into a switch from a PC, find your way around with `?` and Tab, move between user EXEC, privileged EXEC and global config, then use the `clock` command to practice reading IOS help and error messages.]

## The setup

No IP addressing in this one. It's one cable:

| From | Port | To | Port | Cable |
|---|---|---|---|---|
| PC1 | RS 232 | S1 | Console | Console (light blue) |

Then PC1 > Desktop > Terminal, keep the default port settings, and press Enter at "Press RETURN to get started!"

## What I typed, and why

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

[One short paragraph: what `?` shows at `S1>` versus `S1#`, why `config` worked as well as `configure`, and what you noticed about the prompt in each mode.]

## The lab's questions

[Answer each one in your own words.]

- What is the setting for bits per second? [ ]
- What is the prompt displayed on the screen? [ ]
- Which command begins with the letter "C" (at `S1>`)? [ ]
- Which commands are displayed for `t?` and for `te?` [ ]
- What information is displayed for the `enable` command? [ ]
- What displays after pressing Tab on `en`? What would happen if you typed `te` at the prompt? [ ]
- How does the prompt change after `enable`? How many commands start with "C" now? [ ]
- What message is displayed after `configure`? How does the prompt change? [ ]
- What does `show clock` display, and what year? [ ]
- What do `clock`, `clock ?` and `clock set ?` display? [ ]
- What was returned for `cl<Tab>`, `clock`, `clock set 25:00:00` and `clock set 15:00:00 32`? [ ]

## Where I got stuck

[Be specific. A few moments the log shows, if they were part of it:]

- [`clock set 15:00:00 01/31/2035` was rejected. What format did IOS want instead, and how did `?` show you?]
- [At 11:47 I was back at `S1>` and had to `enable` again, about 17 minutes after my last command. What logged me out?]
- [`cl` plus Tab didn't finish the word, so I typed `ock` on its own line. Why didn't Tab complete `cl`, and why didn't `ock` work?]

## Proof it worked

![show clock after setting the date](/assets/img/lab-01/show-clock.png)

![Check Results](/assets/img/lab-01/check-results.png)

## What I'd tell someone doing this next

[Three bullets, max.]
