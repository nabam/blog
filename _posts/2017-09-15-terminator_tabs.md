---
layout: post
title:  "Fixing Terminator Tabs Appearance"
categories: workstation
tags: linux workstation terminator gtk
---

I was looking for an iTerm2 replacement after I switched to Ubuntu from OS X.
I'm using terminal splits heavily but don't want to use
tmux as my primary terminal emulator. So I've found a project called
[Terminator](https://gnometerminator.blogspot.ru/p/introduction.html).
It supports almost all features that I was using in iTerm2 including
splits and broadcast input. It's written in Python with PyGTK. One
of the things I didn't like was an appearance of tabs in HiDPI
environment.  My laptop has a HiDPI display and gnome
scale factor is set to 2. So with scale factor 2 tabs looks like this:

![ugly tabs](/assets/images/content/ugly_tabs.png)

<!-- more -->

They are huge, vertical paddings are too high. Well, it's open source, right?
After some digging it turned out that [gtk-3 styles are described with a pure CSS](https://developer.gnome.org/gtk3/stable/chap-css-overview.html).
And it's possible to override almost every design aspect of any GTK-3 application.
Overrides can be defined in `~/.config/gtk-3.0/gtk.css` file. That is what I ended
up with there:

*UPD 2018: This style is supposed to work on bionic*
{% gist nabam/cd8cfbff69e3ca37594f7345281022ae gtk.css %}
<details><summary><i>Original snippet</i></summary>
<p>
{% gist nabam/efcd7e3aaf649a88082a516de5027e89 gtk.css %}
</p>
</details>

That is how it looks:

![neat tabs](/assets/images/content/neat_tabs.png)
