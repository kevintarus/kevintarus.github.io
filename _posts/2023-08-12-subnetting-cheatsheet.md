---
title: Subnetting Cheatsheet
author: Tarus
date: 2023-08-12 21:23:00 +0300
categories: [Cheatsheets]
tags: [subnetting, hosts, network, ip address, cidr]
---

I compiled this Subnetting Cheatsheet for easy reference and reminder on how to subnet ip addresses.

## Formulars
2^h = number of hosts; where h is the number of host bits

2^h - 2 = number of usable hosts; 2 addresses (network and broadcast address) are subtracted

2^n = number of subnets; where n is the number of borrowed bits from the host portion in order to create subnets

## Cheatsheets

![Alt text](/assets/subnetting/image.png)

- From the above diagram, the top 4 rows represent the cidr notation. For example you are given a /15 network, the subnet is in the same column at the bottom. Since it is in the second row, the subnet 254 will be in the second octet (255.254.0.0). If it is /26 which is in the fourth row, the subnet will be 255.255.255.192

- Other examples include:
1. /20 - 255.255.240.0 
2. /27 - 255.255.255.224

## FULL CHEATSHEET

![Alt text](/assets/subnetting/image-1.png)

![Alt text](/assets/subnetting/image-2.png)

![Alt text](/assets/subnetting/image-3.png)

Class A: Have a default subnet mask
Class B: Have a default subnet mask
Class C: Have a default subnet mask
Class D: reserved for multicast 
Class E: Experimental purposes

Classless address - Doesn't use the default subnet address, provide good allocation of ip addresses
Classful address - Uses the default subnet address, can lead to ip address exhaustion

127.0.0.0 - 127.0.0.255 == Loopback address (Used for network testing)