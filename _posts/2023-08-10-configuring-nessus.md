---
title: Configuring Nessus to Perform Security Vulnerability Scans on Devices
author: Tarus
date: 2023-08-10 15:16:00 +0300
categories: [Blog, Labs]
tags: [nessus, windows, vulnerabilities, network]
---

## What is Nessus
- Nessus is a security scanning tool which scans a computer and raises an alert if it discovers any vulnerabilities that malicious hackers could use to exploit or gain access to a system in a network.
- It can scan for security vulnerabilities in devices, applications, operating systems, cloud services and other network resources.
- Nessus identifies software flaws, missing patches, malware, denial-of-service vulnerabilities, default passwords and misconfiguration errors, among other potential flaws. When Nessus discovers vulnerabilities, it issues an alert that IT teams can then investigate.

- In this lab, I will be using Nessus Essentials which is the free version but still has lots of features.

## Features
Some of its features include:
- Basic Network Scan
- Malware Scan
- Web Application Tests
- Mobile Device Scan
- Credentialed Patched Audit
- Active Directory Scan

![Alt text](/assets/nessus/image.png)

## Setup

Go to there website and download Nessus Essentials, chose your appropriate OS

![Alt text](/assets/nessus/image-5.png)

Once it is downloaded, run the program to install Nessus. In my case, I am on linux so i used dpkg -i command to install the .deb package 

![Alt text](/assets/nessus/image-6.png)

Go to a web browser and copy the weblink shown after installing Nessus

![Alt text](/assets/nessus/image-7.png)

Choose Nessus Essentials

![Alt text](/assets/nessus/image-8.png)

Create user account and password after registering your email

![Alt text](/assets/nessus/image-9.png)

![Alt text](/assets/nessus/image-10.png)

Wait for all the plugins to install. Once installed click on New Scan

![Alt text](/assets/nessus/image-11.png)

Pick on any features you want to run. In my case, I picked Basic Network Scan

![Alt text](/assets/nessus/image-12.png)

- In the target section, you can input:
1. A single ip address => 192.168.100.1
2. A range of ip addresses => 192.168.100.10-192.168.100.230
3. A whole network address => 192.168.100.0/24 

- Save the results and wait for scanning to complete

![Alt text](/assets/nessus/image-13.png)

- These are some of the results from the scan.
PS: these are hosts from virtual machines so don't try anything silly :)

![Alt text](/assets/nessus/image-1.png)

![Alt text](/assets/nessus/image-2.png)

![Alt text](/assets/nessus/image-3.png)

![Alt text](/assets/nessus/image-4.png)

Nessus is an amazing tool for Security Analysts since:
- It shows the severity of vulnerabilities by rating them
- Gives alot of details regarding the vulnerabilites
- Gives solutions and recommendations to minimise or mitigate those vulnerabilities.
- Gives additional links in order to research further