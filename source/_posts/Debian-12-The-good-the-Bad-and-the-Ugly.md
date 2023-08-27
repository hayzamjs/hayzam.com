---
title: 'Debian 12: The Good, the Bad and the Ugly'
date: 2023-08-26 22:13:58
tags: debian, linux, review, bookworm, linuxmint, zorin, ubuntu
---

# Introduction

In the beginning of 2021, I acquired a new machine with a shiny, new AMD Ryzen 7 5800X CPU, 32 GB of RAM, a 1 TB SSD (along with some spare HDDs). There was also supposed to be a 3070 GPU in the setup, but shipping mishaps resulted in significant damage. I wasn't willing to spend hundreds of extra dollars for a new GPU, so I stuck with my reliable GTX 1060 for the relatively light gaming I engaged in.

<p style="text-align: center;">
    <img width="512px" src="https://imagedelivery.net/SM0H54GQmiDTGcg4Xr4iPA/61e95ca5-3aa0-4bbd-afe4-95d2b584dd00/1692" alt="pc"/>
    <small>Setup as of 2023</small>
</p>

For most of my life, I had been a Windows user. To put it mildly, Windows was almost always the pre-installed operating system on the systems I purchased, and I didn't feel compelled to switch. Although I had encountered macOS on several occasions and admired it, the drawback was the requirement for Apple's proprietary hardware to ensure smooth operation (hackintosh setups always appeared troublesome to me).

Even though I was fairly content with Windows, I arrived at a somewhat peculiar realization. During periods when I wasn't gaming or involved in very light Photoshop tasks, I found myself turning to the Windows Subsystem for Linux (specifically WSL2) for my work. Given that most of my projects were geared towards various Linux-based operating systems, I always felt a sense of familiarity whenever I operated within the WSL2 environment.

So, after nearly 8 years of consistent Windows usage, I made the switch. However, I didn't immediately transition to Debian. It was the beginning of 2023, and I found myself exploring various Linux distributions in what could be called a "distro-shopping" phase. I sifted through several options before stumbling upon [Zorin OS](https://zorin.com/os/). I ended up using it for the majority of the year. Unfortunately, a significant drawback of Zorin OS was the prolonged update process, and I consistently encountered issues with their updater. This problem escalated to a point where I was unable to update the system. In my attempts to resolve this, I may have inadvertently caused some irreparable damage to the system. Frustrated with the situation, I decided to part ways with Zorin OS and sought out a new distribution to try.

# History with Debian

I had used Debian 7 "Wheezy" back in high school (2015?) when the hand-me-down laptop from my dad proved too slow to run Windows. To my surprise, Debian felt incredibly snappy on that machine. I recalled it being exceptionally lightweight. The only significant hiccup I encountered back then was the incompatibility with Intel-based WiFi chips, which meant I had to resort to using a dongle. Aside from that, the overall experience was excellent.

# Debian 12

## The Good

I used [Balena Etcher](https://etcher.balena.io/) to flash the Debian 12 ISO onto a USB drive. The familiar Debian installer greeted me, which was a pleasant surprise. I had anticipated significant changes to the installer since my last use, but it remained largely the same. Installing Debian 12 was a breeze, without encountering any issues. The process was quick and painless.

To my surprise, Debian 12 recognized my WiFi chip immediately. I effortlessly connected to my network without requiring any additional configuration, even though I used the Ethernet port this time. The installation process was unexpectedly smooth; I had braced myself for potential driver-related problems, yet everything functioned seamlessly out of the box.

<p style="text-align: center">
    <img src="https://imagedelivery.net/SM0H54GQmiDTGcg4Xr4iPA/c0784b90-4fd9-4b20-075a-0414a34c4200/1692" alt="desktop"/>
</p>

Staying true to my familiarity with GNOME on Zorin, I chose to stick with it when transitioning to Debian. I enriched my experience by integrating extensions, which augmented the environment's capabilities. The disparity in speed between Debian and Zorin was unmistakable, with Debian notably exhibiting greater swiftness. Remarkably, Debian even surpassed Windows by a considerable margin in terms of performance. Another endearing detail to mention is that, among all the machines my partner has observed me working on, this one received her compliments – a fact I found rather cool.

Upon inspecting the "about" page in GNOME, I noticed that it was indicating the use of Wayland. This revelation prompted me to realize that, by default, Debian installs the nouveau drivers instead of NVIDIA's proprietary alternatives. Although this sufficed for my initial work needs, I encountered a multitude of online recommendations strongly advocating for the installation of NVIDIA's proprietary drivers to achieve enhanced performance. Intrigued, I opted to give this approach a try.

## The Bad

### Multiple GPU Challenges

During my quest to set up Debian 12, I aimed not only to accomplish the installation but also to take things up a notch by configuring two GPUs. My goal was to have a VM with a dedicated GPU passed through, and a separate NVME drive reserved for Windows, allowing me to carry out light photo editing tasks. I possessed two GPUs for this endeavor: a GTX 1060 and a less capable GT 710. While I was well aware that getting the GT 710 to function might be a long shot, I was determined to give it a try.

I turned to online resources to guide me and was surprised to discover that installing the nvidia-drivers was a straightforward process:

```
sudo apt install nvidia-driver
```

However, as the installation progressed, an issue arose: the installation process warned that the GT 710 was a problematic device and might not integrate well with my system. Since my intention was to pass the GT 710 to the VM, I initially brushed off this warning. Unfortunately, this decision led to unforeseen consequences. After the installation, my system encountered significant booting difficulties—although I couldn't discern the exact cause. In order to troubleshoot, I removed the GPU, performed a fresh Debian 12 installation, and this time around, I only inserted the GTX 1060. With the nvidia-driver installed, the process proceeded without a hitch.

<p style="text-align: center">
    <video src="https://i.imgur.com/JA9bqKy.mp4" controls muted autoplay></video>
</p>

Subsequently, I introduced the GT 710 back into the system and seamlessly passed it through to the VM without encountering any hurdles. I managed to install the necessary drivers for it within the Windows environment.

### Package Management

I was reluctant to put this in the "bad" section, but I felt it was worth mentioning and it caused me significant pain especially when it comes to not knowing that some packages on Debian (or the default apt repo's) are a bit out of date and it is not readily apparent.

Navigating the software installation process in the Linux environment, particularly when using a package manager like Apt on Debian, can present its own set of challenges. While Apt does provide a relatively streamlined experience compared to some other package managers, it may not always match the level of simplicity found in alternative methods of software installation. The need to search for the appropriate package, install it, and then initiate the program can introduce additional steps that might seem a tad cumbersome. This process, although not a major inconvenience, does underscore the differences between Linux and other operating systems in terms of software management.

Moreover, delving into the realm of packaging systems further adds complexity to the Linux software landscape. The distinctions and nuances between various packaging systems such as Flatpak and AppImage can be a bit perplexing to grasp initially. Each system comes with its own set of advantages and trade-offs, leaving users to navigate through considerations like sandboxing, compatibility, and maintainability. While these options bring flexibility, they also demand a level of understanding that can be challenging, especially for those accustomed to more straightforward methods of software installation. As the Linux ecosystem continues to evolve, striking a balance between these diverse packaging systems and user-friendly installation experiences could potentially bridge the gap for users seeking a smoother transition.

## The Ugly

### Kernel Update Issues

A few days ago, the 6.1.0-11 kernel version was released, and I received a notification to update to it, as I was on the stable branch. However, this decision turned out to be ill-advised. Upon updating, the boot process led me to a state where it became stuck at a flashing underscore. This was quite alarming to witness, but fortunately, Debian preserves the previous kernel version as a precaution. As a result, I was able to easily revert back to the older kernel version, resolving the issue.

Nonetheless, this incident highlights a problem that requires attention. I'm still uncertain about the cause of this booting problem or how to rectify it. If you have some ideas on how I could go about troubleshooting it, please let me know in the comments.

### Bluetooth Failures

I rely heavily on a Bluetooth controller (a PS5 controller) and a Bluetooth headset for my activities. While the controller generally functions well without any hitches, there are intermittent instances when I encounter an issue. Specifically, I find that there are times when I'm unable to power on the controller or even initiate a device scan – it becomes unresponsive or "stuck." To rectify this situation, I need to go through a series of steps: shutting down the computer, disconnecting the plug, waiting for a brief period, reconnecting the plug, and then booting up again. This recurring problem has led me to consider reverting to Windows due to its impact on my user experience. However, I'm remaining optimistic that I can find a solution to this problem and continue using Linux.

# Conclusion

My journey from Windows to Debian 12 has been quite a ride, filled with some surprises and challenges. It's been nice to see the Debian installer still welcoming me, and the installation process was surprisingly quick and easy – a definite win.

One cool thing was how Debian just knew my hardware, making network setup a breeze. But then, things got a bit tricky when I delved into setting up multiple GPUs and virtual machines. Figuring out GPU compatibility, drivers, and system stability was an adventure in itself.

Debian's speed, especially compared to Zorin and Windows, was a highlight. I could really feel the difference, and it made me more productive. On the flip side, I kind of missed the simplicity of installing software on Windows. Linux's package management has a learning curve, that's for sure.

One thing that's been a bit of a pain is Bluetooth. My PS5 controller and Bluetooth headset occasionally decide to go on strike, making me restart my computer and mess with plugs – not exactly smooth sailing.

To wrap it up, Debian 12 has been a mix of the familiar and the new. It's a reminder that the Linux world has its quirks, but also a ton of potential. As the open-source community keeps growing, I'm hopeful that some of these hiccups will get smoother. All in all, Debian has taken me on a journey through Linux's twists and turns, and I'm excited to see where it goes.
