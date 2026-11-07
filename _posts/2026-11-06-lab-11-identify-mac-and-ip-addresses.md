---
layout: post
title: "Lab 11: Identify MAC and IP Addresses (Packet Tracer)"
tags: [module-13, packet-tracer, addressing]
---

**Module:** IT533 Module 13, addressing
**Tools:** Cisco Packet Tracer, Simulation mode
**Devices:** a router, two switches, a hub, a wireless access point, and the PCs and wireless host on the 172.16.31.0, 172.16.30.0 and 10.10.10.0 networks

## What the lab asked for

Run pings between hosts in Simulation mode and open the PDU Details at every device the packet passes through: the hub, the switches, the access point and the router. At each stop, note which MAC addresses and which IP addresses are in the frame, and watch what changes and what stays the same as the packet crosses from one network to another.

There is nothing to configure in this lab, so there is no command log or saved config. The work is in the answers.

## The lab's questions

My answers, as I wrote them down during the lab.

**1. Were there different types of cables/media used to connect devices?** Yes, straight-through, cross-over, and Serial DCE.

**2. Did the cables change the handling of the PDU in any way?** No

**3. Did the Hub lose any of the information that it received?** No, all data was kept.

**4. What does the Hub do with MAC addresses and IP addresses?** The hub does nothing with the IP and MAC address.

**5. Did the wireless Access Point do anything with the information given to it?** No, the IP and MAC address stayed the same; however, the AP did change the frames from ethernet to wireless.

**6. Was any MAC or IP address lost during the wireless transfer?** Nothing was lost we received 4 replies.

**7. What was the highest OSI layer that the Hub and Access Point used?** The hub reached layer 1 and the AP reached layer 2.

**8. Did the Hub or Access Point ever replicate a PDU that was rejected with a red "X"?** No, the hub or PA never replicate rejected PDU's.

**9. When examining the PDU Details tab, which MAC address appeared first, the source or the destination?** The destination address appears first.

**10. Why would the MAC addresses appear in this order?** The MAC address appears in this order to find out who is sending the request.

**11. Was there a pattern to the MAC addressing in the simulation?** The pattern I saw was that each hop the packets took, the source and destination address changed

**12. Did the switches ever replicate a PDU that was rejected with a red "X"?** Yes, when pinging 172.16.30.2 from 172.16.31.5 the switch sent packets to the router and 172.16.31.4. It also sent packets to the hub which sent it out all ports till it reached the destination.

**13. Every time that the PDU was sent between the 10 network and the 172 networks, there was a point where the MAC addresses suddenly changed. Where did that occur?** The MAC address change occurred when the PDU's reached the router.

**14. Which device uses MAC addresses that start with 00D0:BA?** The routers FastEthernet 1/0 port uses MAC address starting with 00D0:BA8E.

**15. What devices did the other MAC addresses belong to?** Other hosts and router interfaces.

**16. Did the sending and receiving IPv4 addresses change fields in any of the PDUs?** No, IP addresses did not change.

**17. When you follow the reply to a ping, sometimes called a pong, do you see the sending and receiving IPv4 addresses switch?** The IP addresses do switch. The source and destination IP swap places when the receiving hosts reply to the sender.

**18. What is the pattern to the IPv4 addressing used in this simulation?** The pattern is devices on the LAN end in .31.X and the private network IP addresses are end in 10.X.

**19. Why do different IP networks need to be assigned to different ports of a router?** Because the router is forwarding PDU's to different networks and needs to be separated.

**20. If this simulation was configured with IPv6 instead of IPv4, what would be different?** The IP addresses change and the MAC addresses would stay the same.
