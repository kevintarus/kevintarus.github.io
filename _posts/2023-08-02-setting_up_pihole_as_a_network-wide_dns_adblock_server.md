---
title: Setting up my own Recursive DNS Server using Pihole
author: Tarus
date: 2023-08-02 19:57:00 +0300
categories: [Projects]
tags: [pihole, adblocking, linux, unbound, dns]
---

## Pihole
Pihole is a forwarding DNS Server that you can host yourself that blocks network-wide ads when you attempt to visit web pages and open applications.

## Explanation
If you type in the website kevintarus.com, since pihole doesn't know the ip address of the website, it will forward that request onto the next dns server you have configured for example, Google's DNS(8.8.8.8). That dns server will forward the ip address of kevintarus.com through pihole and into your web browser. When those requests get to pihole, it will check the adblock list and filter out some know ad-serving requests then sends the final webpage to the user.

In this, we will do some tweaking and set it up as a recursive dns server by using unbound. When you ask pihole where is kevintarus.com and if it doesn't know the answer, it will seek out the authoritative dns server of kevintarus.com and get the answer directly from them rather than using a third party DNS like google. 

On the very first request to a website, it will take longer than usual but later it will cache the website info for future use so that its much faster the next time you load the same website.

## Benefits
- Third party DNS servers will no longer be able to compile a list of your internet browsing history based off the webistes you visit
- You will be safer from dns spoofing such as a fake website mimicking legitimate websites
- You can whitelist and blacklist websites
- Be able to monitor and analyse your own home network traffic 

## Tools I Used
A Virtual Machine (Ubuntu Server 22.04)

I recommend using: 
- The cloud (if you have money)
- Rasberry Pi
- Installing Proxmox which is a type 1 hypervisor on an old machine

## Steps I Did
1. Download and set up Ubuntu Server 22.04 (use bridged adapter)

![Alt text](/assets/pihole/image-3.png)

2. Install Pihole from the terminal: sudo curl -sSL https://install.pi-hole.net | bash

![Alt text](/assets/pihole/image-4.png)

![Alt text](/assets/pihole/image-5.png)

![Alt text](/assets/pihole/image-6.png)

![Alt text](/assets/pihole/image-7.png)

![Alt text](/assets/pihole/image-8.png)

![Alt text](/assets/pihole/image-9.png)

3. Set the Web Admin Password: pihole -a -p "input your password here"

   Go to your browser and type: http://192.168.1.1/admin/login.php  (replace it with your ip address for the vm)

![Alt text](/assets/pihole/image-10.png)

4. Install Unbound DNS - sudo apt install unbound

5. Create Unbound Configuration File - sudo nano /etc/unbound/unbound.conf.d/pi-hole.conf

6. Copy the config code from [here](https://docs.pi-hole.net/guides/dns/unbound/) and paste it in /etc/unbound/unbound.conf.d/pi-hole.conf 

7. Restart Unbound to apply Configuration - sudo service unbound restart

![Alt text](/assets/pihole/image-2.png)

8. Disable Forwarding DNS in PiHole by unchecking all the boxes

![Alt text](/assets/pihole/image-1.png)

9. Set Custom DNS in PiHole by putting your localhost address - 127.0.0.1#5335

![Alt text](/assets/pihole/image.png)


After all this steps, you can configure the DNS server address to be the vm's address by putting it:
- In your router's web interface for all devices in the network
- On individual devices.

## Results

![Alt text](/assets/pihole/image-11.png)

![Alt text](/assets/pihole/image-12.png)

In the above diagram, I set up google.com as a blacklist site

![Alt text](/assets/pihole/image-13.png)

The result above shows google.com access from a connected client was blocked.