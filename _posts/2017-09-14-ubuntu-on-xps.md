---
layout: post
title:  "Fun with Ubuntu on Dell XPS 13"
categories: workstation
tags: linux dell laptop workstation
---

I haven't used Linux on a workstation since 2011 when I switched to Mac.
Because of various reasons I've decided to move back and this May
I replaced my MBP with a fancy new [Dell XPS 13 (9360)](http://www.dell.com/en-us/work/shop/dell-laptops-and-notebooks/xps-13-developer-edition/spd/xps-13-9360-laptop/cax13w10p7b5122Ubuntu)
laptop. This shiny computer comes with a preinstalled Ubuntu 16.04. Of course
the experience was quite different from one you get after unboxing an Apple computer.

![dino-mlk2](/assets/images/content/Dell-XPS-13-Ubuntu.jpg)

<!-- more -->

I first powered it on while being in the office. Customized Ubuntu installer
appeared and when I entered 802.1x credentials for our secure wifi
it just crashed. Machine rebooted with no users configured and root
login disabled. That's nice, I thought. It took me some time to setup an
USB Stick with vanilla installer. After I've figured out that there is a
recovery partition, but it wasn't available in the EFI boot menu.
Something wasn't working properly on the vanilla installation so I decided to
reinstall it from this recovery partition now using WIFI with a preshared key.
Installation went fine except OEM installer didn't ask me if I want to
encrypt partitions so later I would reinstall it again.

I also got a bunch of accessories from dell:
[Dell TB 16](http://www.dell.com/en-us/work/shop/dell-business-thunderbolt-dock-tb16-with-240w-adapter/apd/452-bcnu/pc-accessories)
Thunderbolt dock station, which surprised me with it's size and weight,
and
[Dell
DA200](http://accessories.ap.dell.com/sna/productdetail.aspx?c=sg&l=en&s=bsd&cs=sgbsd1&sku=470-ABNL) mobile Thunderbolt adapter.
I plugged my screen, network, keyboard and mouse in TB16 and attached it
to the laptop. Only screen worked. Seriously? In an hour it turned out
that I had to change TB security settings in EFI setup, because
it only works under Windows with special app installed with default ones.

![tb16](/assets/images/content/tb16.jpg)

So far so good!

Next thing I figured out was that HiDPI support in Linux sucks. In Unity
interface scaling works just fine when you have one screen or multiple
screens with the same DPI (except for old GTK, Wine, Java and some other
things that require custom tweaks). But when you connect a display with
different DPI you are getting into trouble! At first none of window
managers supports different DPI on multiple screens. At all. Well,
Gnome on Wayland supports it but it's immature yet and scaling works only
for Gnome apps. It means that when you launch or move something to a
screen with a lower DPI it will be huge or the way around.
OK, I'm ready for compromises, what if I downscale laptop's resolution to
match external screen's DPI. Unfortunately it's not enough. After changing
scale factor only gnome apps resize. The rest you will have to restart
to fetch new configuration. For me the rest are Chrome, all
chromium-based apps, Telegram, IDEA, gVIM and others. So there are 2
options: restart everything after you connect or disconnect external
display or live with blurred laptop screen with downscaled resolution.

For anyone who is looking for a Linux laptop **I would strongly recommend
not buying one with HiDPI screen** It's just a pain in the ass. While I
was using OS X I didn't even know that such a problem exists.

So, I got my screen and laptop working, as well as USB ports on a dock.
After doing some stuff I figured out that I had no network
connectivity. Again, more digging. It looked like something was wrong
with a NIC in the dock station. I hit a bug related to dock's USB controller driver
[LP:1667750](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1667750).
There was a patch, but XHCI is compiled into a kernel, so there is no
way to build a DKMS package and the least thing I wanted was to maintain
my own kernel build. So I had to apply a workaround and limit NIC speed
to 100Mbit/s. BTW in August it eventually got into a stable kernel and already
backported to Ubuntu mainline.

Finally I was able to get back to work.

![da200](/assets/images/content/da200.jpg)

Later I got home and tried to attach screen at home with DA200 adapter.
And failed. Again, a lot of investigation. It worked in all modes except
Full HD. It even worked with interlaced Full HD (which made my eyes
bleeding). Fortunately there was a bug report for this one also.
[Bug 93578](https://bugs.freedesktop.org/show_bug.cgi?id=93578). In
DA200 Dell are using DP-HDMI converter that is not following Display
Port specs. I've learned a lot about Display Port that night. Seriously,
[ICCE Presentation on VESA DisplayPort](http://www.vesa.org/wp-content/uploads/2011/01/ICCE-Presentation-on-VESA-DisplayPort.pdf)
is fascinating. At least this problem I was able to fix by creating a
dkms package with patched i915 driver. I read through an intel drm
kernel mail group and was amazed by an amount of work Intel folks
were doing to bring their new stuff to the kernel. Currently it works
properly only with hwe-16.04-edge (4.11.0) kernel on Xenial and I'm
not sure if it's going to be backported to the mainline.

Of course I faced other issues later. For example [BUG
99295](https://bugs.freedesktop.org/show_bug.cgi?id=99295) is the nice
recent one (fixed in hwe-16.04-edge). But I have no regrets. I was really
missing those insides you get every time something requires a fix while
using OS X.

![screenshot](/assets/images/content/screenshot.png)
