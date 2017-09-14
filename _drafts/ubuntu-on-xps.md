---
layout: post
title:  "Fun with Ubuntu on Dell XPS 13"
categories: workstation
tags: linux dell laptop
---

I haven't used Linux on desktops since 2011 when I switched to Mac.
Bacause of various reasons I've decided to go back to it and this May
I switched from MBP to a fancy new [Dell XPS 13 (9360)](http://www.dell.com/en-us/work/shop/dell-laptops-and-notebooks/xps-13-developer-edition/spd/xps-13-9360-laptop/cax13w10p7b5122ubuntu)
laptop with preinstalled Ubuntu 16.04 on it. Of course the experince was quite different from one
you get after uboxing an Apple computer.


I first powered it on in the office. Customized ubuntu installer
appeared and when I entered credentials for our secure wifi with 802.1x
it just crashed. Machine rebooted with no users configured and root
login disabled. That's nice, I thought. It took me some time to setup a
vailla installer to an USB stick. After I've figured out that there is a
recovery partition, but it wasn't available in the efi boot menu.
Something didn't work properly with vanilla installation so I decide to
reinstall it from this recovery partition using wifi with a pre-shared key.
Installation wen fine except OEM installer didn't ask me if I want to
encrypt a partition so later I would reinstall it again.
