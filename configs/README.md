# Device configs

One folder per lab. Each file is the `show startup-config` output from that device after the lab was finished and saved, so the history of this folder is the history of my lab work.

Passwords in these files are the Packet Tracer textbook values (`class`, `cisco`), never real ones.

| Folder | Lab | Devices |
|---|---|---|
| drill-01 | Cisco drill 1: modes, passwords, banner, interfaces, saving | S1 (2960), R1 (ISR4221) |
| lab-02 | Lab 2: Basic Device Configuration (plus the full command log) | Floor14 (1941), Room-146 (3650) |
| lab-03 | Lab 3: Configure Initial Switch Settings (plus the full command log) | S1, S2 (2960) |
| lab-04 | Lab 4: Configure Initial Router Settings (plus the full command log) | R1 (1941) |
| lab-05 | Lab 5: Basic Switch and End Device Configuration (plus the full command log) | Room-145, Room-146 (2960) |
| lab-06 | Lab 6: Build a Switch and Router Network (plus the full command log) | R1 (ISR4321), S1 (2960) |
| lab-08 | Lab 8: Connect a Router to a LAN (plus the full command log) | R1, R2 (1941) |
| lab-09 | Lab 9: Connect the Physical Layer (command log only: show commands, no config changes) | East (1941), Switch2 |
| lab-10 | Lab 10: Implement Basic Connectivity (plus the full command log) | S1, S2 (2960) |

Lab 7 was a cabling lab with no commands, so it has no folder here; its cable list is in the post.

Three files are running configs instead of startup configs because my last changes came after my last save: lab-05 Room-145 (password encryption and the banner), lab-06 R1 (the SSH settings) and lab-10 S1 (the enable secret fix).
