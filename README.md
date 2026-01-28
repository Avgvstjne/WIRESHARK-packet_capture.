# WIRESHARK-packet_capture.
---

[Watch Lab Wireshark capture](https://youtu.be/YMm08l1yKA0)

---
pdf

---

# This is a lab scenario, of a security analyst investigating traffic to a website.

I analyzed the network packet capture file that contains traffic data related to a user connecting to an internet site.

This filtering of the data was in order to:

* a. Identify the source and destination IP addresses involved in this web browsing session,
* b. examine the protocols that are used when the user makes the connection to the website,
* c. and analyze some of the data packets to identify the type of information sent and received by the systems that connect to each other when the network data is captured.

Walkthrough:

First, I opened the packet capture file and explore the basic Wireshark graphic user interface.   
Second, I opened a detailed view of a single packet and explored how to examine the various protocol and data layers inside a network packet.   
Third, I applied filters to select and inspect packets based on specific criteria.   
Fourth, I filtered and inspected UDP DNS traffic to examine protocol data.   
Finally, I applied filters to TCP packet data to search for specific payload text data.   

Here is an overview of the key property columns listed for each packet:

No. : The index number of the packet in this packet capture file   
Time: The timestamp of the packet   
Source: The source IP address   
Destination: The destination IP address   
Protocol: The protocol contained in the packet   
Length: The total length of the packet   
Info: Some infomation about the data in the packet (the payload) as interpreted by Wireshark   

Not all the data packets are the same color. Coloring rules are used to provide high-level visual cues to help with the quick classification of the different types of data.   
Since network packet captured files can contain large amounts of data, coloring rules can be used to quickly identify relevant data.

For this lab, I started with the packet where the info column starts with the words 'Echo (ping) request', for a detailed exploration and data filtration to inspect the network layers and protocols contained in the packet. Having entered a filter for traffic associated with a specific IP address the list of packets displayed is now significantly reduced and contains only packets where either the source or the destination IP address matches the address entered. Also, only two packet colors appear here: light pink for ICMP protocol packets and light green for TCP (and HTTP, which is a subset of TCP) packets.

I checked the first packet that lists TCP as the protocol, the upper section of this window contains subtrees where Wireshark provides an analysis of the various parts of the network packet. The lower section of the window contains the raw packet data displayed in hexadecimal and ASCII text. (I observed that the 'details pane' is located at the bottom portion of the main Wireshark window and it can also be accessed in a new window by double clicking a packet), by double-clicking to open or collapse, I checked the first subtree in the upper section. This starts with the word Frame. This provides details about the overall network packet, or frame, including the frame length and the arrival time of the packet. I collapsed the frame subtree and opened the Ethernet II subtree, here, contains details about the packet at the Ethernet level, including the source and destination MAC addresses and the type of internal protocol that the Ethernet packet contains. The Internet Protocol Version 4 subtree provides packet data about the Internet Protocol (IP) data contained in the Ethernet packet. It contains information such as the source and destination IP addresses and the Internal Protocol (for example, TCP or UDP), which is carried inside the IP packet. The source and destination IP addresses shown in the Internet Protocol Version 4 subtree (Internet Protocol Version 4 (IPv4)) match the source and destination IP addresses in the summary display for this packet in the main Wireshark window. The Transmission Control Protocol subtree provides detailed information about the TCP packet, including the source and destination TCP ports, the TCP sequence numbers, and the TCP flags, clicking on flags here provides a detailed view of the TCP flags set in this packet.

Next task is to use filters to select packets

I used filters to analyze specific network packets based on where the packets came from or where they were sent to and explored how to select packets using either their physical Ethernet Media Access Control (MAC) address or their Internet Protocol (IP) address, a filtered list is returned that contains only packets that were sent to 142.250.1.139.

Next, I used filters to select and examine DNS traffic, drilling down into the protocol to examine how the DNS packet data contains both queries (names of internet sites that are being looked up) and answers (IP addresses that are being sent back by a DNS server when a name is successfully resolved). I entered a filter to select UDP port 53 traffic. DNS traffic uses UDP port 53, so this will list traffic related to DNS queries and responses only.   
Using additional filters to select and examine TCP packets. I search for text that is present in payload data contained inside network packets. I entered a filter to select TCP port 80 traffic (TCP port 80 is the default port that is associated with web traffic) and quite a few packets were created when the user accessed the web page.
