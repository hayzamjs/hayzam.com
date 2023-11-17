---
title: Replacing My Home/Office Lab with One Box
date: 2023-11-17 23:20:42
tags: homelab, firewall, openwrt, router, adguard, wireguard
---

## The Initial Setup at Alchemilla.io

At my software solutions startup, [Alchemilla.io](https://alchemilla.io), I had set up what I'd call an office-lab—though it feels a bit odd to say, compared to the usual 'homelab'. This setup ran on multiple devices:

* **An old Dell Optiplex with a 3rd generation i5 and 8GB of RAM, operating on Debian.**
  
  <img src="https://i.imgur.com/oj26dLa.jpg" alt="A cat with an Optiplex attached" width="200"/>
  
  This machine was the workhorse for running various services. It hosted multiple Docker containers for tools like AdGuard Home, OPNSense, PiVPN for WireGuard, and some other simple scripts. I even set up a Cloudflare tunnel, given our CGNAT constraints.

* **A TP-Link AP (AX3000)**
  
  This router served as the office's sole wireless access point. It was tethered to the OPNSense box via a NIC and functioned as a 'dumb AP'.

* **A SIM gateway**
  
  This was intended to enable the use of a 4G connection as a backup. However, I never actually utilized this feature because OPNSense had compatibility issues with it. Additionally, it was meant to provide call and text functionality for the associated number.

## Confronting the Challenges

### Tackling Hardware Issues

The hardware setup posed several issues. Firstly, the Dell Optiplex was a significant power consumer. My pre-setup electricity bills were around $100 a month, but post-setup, they jumped to about $150. The TP-Link AP also had its quirks; it would occasionally lose connection to the OPNSense box, requiring a reboot to resolve the issue. Additionally, it had intermittent problems like the 5GHz band occasionally failing and the 2.4GHz band's sluggish performance.

Another concern was the Dell Optiplex's design. Originally intended as a desktop, it was loud and prone to overheating. I had to stash it in a closet to mitigate the noise, but this only exacerbated the overheating issue.

### Software Struggles

My software choices were predominantly open-source, with the exception of the TP-Link AP and Cloudflare tunnels/Tailscale (which is semi-open-source). Performance-wise, I encountered no significant issues. However, the ongoing maintenance of updating operating systems, containers, and the like was becoming burdensome. I desired a seamless operation, but despite the individual strengths of each component, the overall setup lacked cohesion.

## Exploring Alternative Solutions

### Evaluating New Devices

I considered several options to address the issues I was facing:

1. **Replacing the Dell Optiplex with a more power-efficient machine**: This seemed like a straightforward solution, but it wouldn't solve the software maintenance problems I was experiencing.

2. **Upgrading the TP-Link AP to a more reliable model**: While this might fix the connectivity issues, it wouldn't address the challenges posed by the Dell Optiplex.

3. **Switching to a more compatible SIM gateway**: This could potentially improve the 4G backup functionality, but again, it wouldn't resolve the Optiplex's problems.

In short, it was a complicated situation. I did explore some promising devices:

- [Raspberry Pi 4](https://www.raspberrypi.org/products/raspberry-pi-4-model-b/)
- [Netgate 1100](https://shop.netgate.com/products/1100-pfsense)
- [OPNsense DEC675](https://shop.opnsense.com/product/dec675-opnsense-desktop-security-appliance/)
- [Turris Omnia](https://www.turris.com/en/products/omnia/)

These are all capable products, but the thought of juggling various software components to make them work together was daunting. I was leaning towards a more plug-and-play solution, requiring minimal intervention post-setup.

**A Closer Look at Turris Omnia**:

The Turris Omnia caught my attention, but it had its drawbacks. The cost was a bit steep relative to its specs, particularly since I was now looking for a solution with robust PBX functionality. The Omnia's 2-core CPU seemed underpowered for my needs. While its software is open-source and well-designed, it lacked key features I was seeking. Additionally, the prospect of configuring a PBX system on it seemed more hassle than it was worth.

## Realizing Software's Central Role

### The Intuitiveness Dilemma

I came to understand that my challenges with software intuitiveness would remain, regardless of the hardware choice. I'm aware that "intuitiveness" can be subjective, but for my needs, it meant being able to provision WireGuard clients, configure firewall rules, and set up and edit my PBX configuration with minimal effort. These are tasks I frequently engage in, and I desired a more streamlined process for handling them.

## Collaborative Efforts in Innovation

### Venturing into Multi-Service Business Gateway

Around this time, my friends, who were also experiencing configuration fatigue, showed interest in creating a [multi-service business gateway](https://en.wikipedia.org/wiki/Multi-service_business_gateway). This concept was new to me, so I had to look it up. It turned out to be precisely the kind of system I envisioned for my own office. However, our interests diverged slightly: they were more focused on the hardware aspects, while my curiosity leaned towards the software side. Recognizing our complementary perspectives, we decided to collaborate on this project.

#### Hardware Considerations

Finding a high-quality ARM-based router board that met our specific requirements proved to be more challenging than anticipated. While there are numerous options available in the market, identifying a vendor that offered a board with at least a 4-core CPU and 2 GB of RAM, along with official support for OpenWRT, required diligent searching. However, after a thorough evaluation of various suppliers, we were fortunate to find one that not only satisfied our specifications but also instilled confidence in their product's quality and reliability.

#### Software Perspectives

As I previously mentioned, OpenWRT was our preferred choice for embedded systems, and arguably the only feasible option. It's a common misconception that OpenWRT is just "router firmware," but it's actually much more. OpenWRT is a full-fledged Linux distribution with a package manager and a web interface, and it's one of the most widely-used embedded Linux distributions, supported by a large community and a vast array of available packages.

While the operating system itself was ideal, its management GUI, although functional, left something to be desired. The structure of LUCI and UCI (the underlying configuration interface) is commendable, enabling configuration through an RPC endpoint without requiring LUCI or command-line interaction. However, the user interface felt outdated and lacked the intuitiveness we were aiming for. Our goal was to develop a more modern, intuitive, and user-friendly interface for OpenWRT.

## Introducing Difuse

### Developing a New Interface

Armed with my knowledge of being able to control the entire system with the RPC endpoint, I set out to create a new interface. I wanted to build something that would be easy to use and maintain, and that would allow me to configure the system without having to use the command line. I also wanted to be able to easily add new features and functionality to the system without having to rewrite the entire interface.

### The Initial Prototype

[![Difuse Prototype](https://i.imgur.com/ElLOva5.png)](https://i.imgur.com/ElLOva5.png)

The initial prototype was rough, nothing was really figured out well. It only had a few functional pages, and the code was a mess. However, it was enough to get the idea across, and it was enough to get the ball rolling.

### Where We Are Now

If I had to list out every feature that Difuse has, this blog post would be far too long. Instead, I'll list out some of the more notable features that I think are going to be useful to people almost universally.

### Everything is just a click away

Be it configuring your PPPoE connection or WiFi AP, everything is just a click away. No more digging through menus to find what you're looking for. Let's look at the WiFi AP configuration page as the first example:

[![Difuse WiFi AP Configuration](https://i.imgur.com/vAeVJDR.png)](https://i.imgur.com/vAeVJDR.png)

Now let's go through a little bit of what we're very excited about.

## Adguard Home

Adguard is a DNS-based ad blocker that can be used to block ads on your entire network. It's a great way to block ads on your entire network without having to install ad blockers on every device. It's also a great way to block ads on devices that don't support ad blockers, like smart TVs and game consoles. The integration fits nicely in an iframe, and all the updates are done along with the full firmware (which is only about 60 megabytes all in)

[![Difuse Adguard Home](https://i.imgur.com/WnddSN1.png)](https://i.imgur.com/WnddSN1.png)

## Hassle-free policy based routes

For some reason my ISP blocks access to **raw.githubusercontent.com** and as a full time developer that sucks, I dont want to enable and disable a VPN or connect to one indefinitely on each of my servers/PC that wants to access it, I want it to *just work*. On plain openwrt there are some nifty tricks that you can do to achieve the same thing (MWAN3, PBR are a few of them) but I bet you can't do it this fast.

<video width="100%" height="100%" controls>
  <source src="https://i.imgur.com/yRfpfqS.mp4" type="video/mp4">
</video>

## Simple yet powerful firewall

Difuse's firewall is designed for simplicity and power, built on nftables for high performance. Key features include:

- **Simple "Aliases"**: Similar to OPNSense, allowing lists of IPs and GeoIP support for Traffic Rules.
- **Bandwidth Control**: Limit bandwidth for MAC or IP addresses, ideal for managing data caps or device-specific bandwidth.
- **Simple Intrusion Prevention**: Similar to fail2ban, useful for blocking brute-force attacks.
- **One-to-one NAT**: Utilize multiple IPv4 addresses with internal IP mapping, powered by nftables.

![Difuse Firewall](https://i.imgur.com/oiODhba.png)
![Difuse Firewall Aliases](https://i.imgur.com/95ztNjv.png)

## Multiple VPN Support

Difuse currently supports WireGuard, IPSec, and Tailscale, with OpenVPN coming soon. Features include:

- **Fast Setup**: WireGuard server setup in under 30 seconds, client addition in less than 5.
- **Ease of Use**: Tailscale and IPSec setup is straightforward.

<video width="100%" height="100%" controls>
  <source src="https://i.imgur.com/1HVFaSC.mp4" type="video/mp4">
</video>

## Let's Encrypt Certificates & Dynamic DNS

Difuse simplifies the creation of valid TLS certificates using a wrapper around [acme.sh](acme.sh). Features include:

- **Easy Certificate Creation**: Just enter your domain and click a button.
- **Dynamic DNS with Difuse Box**: Free dynamic DNS domain for Difuse Box owners.

![Difuse ACME](https://i.imgur.com/vzq4aoy.png)

## Additional Services

New services added in Difuse:

- **Samba**: Easy management of Samba shares via web interface. You can use an M.2 SSD or USB drive for storage and share it over the network.
- **TOR**: One-click TOR proxy setup for selective .onion domain access.
- **IPFS**: Set up an IPFS gateway on a storage device and use that as a gateway network-wide.
- **Bandwidth Monitoring and DPI Dashboard**: Comprehensive per-device bandwidth monitoring and DPI dashboard. The DPI dashboard right now supports only analytics but we're working on adding more features to it.

## PBX Features

Difuse's PBX offers:

- **Remote Provisioning for Extensions**
- **CDR with Statistics and Call Recording**
- **Simple Flash Operator Panel**
- **Unlimited Extensions Without Licensing Fees**
- **4G LTE Module Support**: For calls and SMS.

## Upcoming Developments

- **Advanced DPI with SD-WAN Features**: Enhancements in progress.
- **New DMSBG-100 Version**: Upcoming model with a stronger CPU, WiFi 7, and more.

## Conclusion

![Difuse Dashboard](https://i.imgur.com/vKF3I9v.png)

We've been diligently working on Difuse for a substantial period, quietly refining our product. During this time, we've provided our device to various customers, some managing over 80+ devices seamlessly. As we celebrate the first anniversary of this project, our excitement is palpable. The journey of Difuse so far has been a source of immense pride for our team, and we look forward to the opportunities that lie ahead.

To discover more about Difuse, we invite you to visit our website at [difuse.io](https://difuse.io), or engage with us and our community on our [Discord server](https://discord.gg/3rSypcJeP7). For any inquiries or direct communication with our team, please email me at [hayzam@difuse.io](mailto:hayzam@difuse.io).

We are also thrilled to announce that we are growing our team! If you are passionate about cutting-edge technology and keen to contribute to an evolving project, we encourage you to join us. For more details about career opportunities, please visit our website or get in touch via email.