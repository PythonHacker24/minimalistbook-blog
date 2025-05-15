+++
category = "technical"
title = 'Networking Fundamentals for Linux Administrators — A Suckless and Concise Explanation'
date = 2024-01-10
+++

Statistics are clear on the fact that **96.3%** (while writing this article) of the servers use Linux as their Operating System which is no doubt what every other Linux user on this Earth expects. I believe that the Linux Administrator has to take the shot about the configuration of Networking in Linux Based Server. Some of the underlying concepts remain the same for any other distros but it is mainly intended for Linux.

*“An idiot admires complexity, a genius admires simplicity, a physicist tries to make it simple, for an idiot anything the more complicated it is the more he will admire it, if you make something so clusterfucked he can’t understand it he’s gonna think you’re a god cause you made it so complicated nobody can understand it. That’s how they write journals in Academics, they try to make it so complicated people think you’re a genius” — Terry Davis, Creator of Temple OS*

Prior Statements before proceeding: I would like to keep it simple and suckless to make it a real practical and useful article which would get your things done. Use this as a reference or guide to proceed with. This contain less about the command and more emphasis on consice theorotical explanation of networking topics in the Linux perspective.

## Introduction to Linux Networking
Networking is at the heart of Linux and is expandable through Kernel modules as per the user’s requirements. To work over the networks, one system must continuously run server processes in the background. These are called **“daemons”**. Example: **“named”** which translates IP addresses to human-readable names.

Unix networking commands are based on Internet Protocols which are standardised as per the industry requirements. Hence, these support the TCP/IP stack with most of its commands. So any network engineers can have a good familiarity with the underlying processes happening.

## The core of the TCP/IP stack — Essentials for Linux Networking

TCP/IP stack is a suite of communications protocols that define how different computers can talk. TCP refers to the **Transmission Control Protocol** which is a reliable way of sending packets in the network and ensuring that the packet reaches safely. More of the protocols that come under the TCP/IP protocol suite are:

- [Address Resolution Protocol (ARP)](https://en.wikipedia.org/wiki/Address_Resolution_Protocol)
- [Internet Control Message Protocol (ICMP)](https://en.wikipedia.org/wiki/Internet_Control_Message_Protocol)
- [Point-to-Point Protocol (PPP)](https://en.wikipedia.org/wiki/Point-to-Point_Protocol)
- [Reverse Address Resolution Protocol (RARP)](https://en.wikipedia.org/wiki/Reverse_Address_Resolution_Protocol)
- [Simple Mail Transfer Protocol (SMTP)](https://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol#:~:text=The%20Simple%20Mail%20Transfer%20Protocol,send%20and%20receive%20mail%20messages.)
- [Simple Network Management Protocol (SNMP)](https://en.wikipedia.org/wiki/Simple_Network_Management_Protocol)
- [User Datagram Protocol (UDP)](https://en.wikipedia.org/wiki/User_Datagram_Protocol)

(I have provided here WikiPedia Links for all of them. It’s not like I don’t want to explain them at all, it’s just I don’t want to explain them here. It’s a quick guide so WikiPedia I found the most relevant source for you to go into depth and research more)

## IP Addressing Concepts for Linux Networking
**IP (Internet Protocol)** Addresses are universally recognised concepts and are used to differentiate devices on the Network. There are two types of IP Addresses: IPV4 and IPV6.

- **IPV4:** 4 bytes (32-bits) Address, each byte splitted with a period notation. Contains a network part and host part. Network goes on the left and Host goes on the right side. The biforgation is made with the Subnet mask which separated them. More reference for table on WikiPedia Link: [Classful Network](https://en.wikipedia.org/wiki/Classful_network)
- **IPV6:** 16 bytes (128-bits) Address, which is more advance and next version of IPV4 which solves the problem of running out of IPs. IPV4 addresses can be packed to IPV6.
The Concept of **CIDR** extends the use of Subnets and removes most of the boundations put forward by the Classful Network. Example, 192.168.32.1/24 and 128.66.128.1/17 use CIDR notation.

ISPs provide mostly provide **Dynamic Addresses** to the users. These IP address may change without warnings so incase you need a **Static IP address** for any purpose, contact the ISP to allocate a Static IP address. These address don’t change and hence, things like DNS registration of IP address becomes more easy since the IP is not gonna change.

## Gateways and Routing for Linux Networking
A Gateway stands as a resolution for the address that are not on the Network and routes the traffic out into the Internet. Each portion of a network that is under a separate local administration is called an autonomous system (AS).

### Gateway Protocols

EGP (Exterior Gateway Protocol)
BGP (Border Gateway Protocol)
RIP (Routing Information Protocol)
Hello Protocol
OSPF (Open Shortest Path First)
Routing Daemons exists in the Linux System like **quagga** and **GNU Zebra** which work with these protocols and handle the routing configuration of the system. **routed**, a network routing daemon uses RIP to allow a host to function as only an interior gateway and manages the Internet Routing Tables

**Routing Tables:** Routing tables provide information needed to route packets to their destinations like the destination network, gateway to use, the route status as well as the number of packets transmitted.

## Name Service — DNS and BIND for Linux Networking
**DNS (Domain Name System)** is a distributed database of information about the hosts on a network. It is responsible for resolving the IP Addresses of domain names provided by the user and communicate with the right client. **BIND** refers to **(Berkeley Internet Name Domain)** which is a popular implementation of DNS.

The nameserver of a domain is responsible for keeping the names of the machine in its domain. Other nameservers on the network forward requests for these machines to this nameserver.

## Configuring TCP/IP for Linux Networking
Network Interfaces are the ways in which the softwares uses the hardware to achieve it’s purpose. It depends on the Network Card installed, like a Wireless Network Card or an Ethernet Network Card. With ip command, you can configure the network interface of the device like assigning anIP address, netmask, etc.

## Firewalls and Masquerading
A firewall is responsible for protecting the internal network from other sources with configurations and rules to determine weather the packet to allow or block. Firewalls can be applied on the gateway to protect the network from Internet Threats or on the Local System to protect the single system from network based attacks. iptables command on Linux provides a way to configure rules in the system.

## NFS (Network File System) for Linux Networking
The **Network File System** which is referred as NFS is a protocol for the usage of network attached storage devices to mount to the system as they where on there local system. NFS is an **RPC-based** application-level protocol.

The /etc/exports file is the NFS server configuration file; it controls which files and directories are exported and which kinds of access are allowed. Names and addresses for clients that should be allowed or denied access to NFS are kept in the /etc/hosts.allow and /etc/hosts.deny files.

NFS Server daemons, called nfsd daemons, run on the server and accept RPC calls from clients. NFS servers also run mountd daemon to handle mount requests. Clients use **rpcbind** daemon to work with NFS server.

## Conclusion
These were the absolutely essential concepts for Linux Network written in as concise and suckless as possible. I would consider writing each of these concept in-depth in other articles. This was a quick reference for engineers on Network Concepts for Linux as well as a beginning guide starting to learn Networking for Linux.
