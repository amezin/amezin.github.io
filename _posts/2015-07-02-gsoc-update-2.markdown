---
layout: post
title: "Pointing devices KCM: update #2"
date: 2015-07-02 23:00:00
categories: kde gsoc
---

For general information about the project, look at [this post]({% post_url 2015-06-16-gsoc-intro %})

Originally I planned to work on the KCM UI at this time. But as I am unsure how it should look like, I started a [discussion on VDG forum](https://forum.kde.org/viewtopic.php?f=285&t=127056), and decided to switch to other tasks.

Currently the KCM looks like this:

![KCM screenshot](/images/kcm.png)

KDED module is, I think, almost complete. It can apply settings from configuration file, and has a method exported to D-Bus to reload configuration for all devices or for some specific device. Of course, it also applies settings immediately when device is plugged in. The only thing that is missing is auto-disabling of some devices (like disable touchpad when there's an external mouse).

As usual, [here is a link to the repository](http://quickgit.kde.org/?p=scratch%2Falexandermezin%2Fpointing-devices-kcm.git).

Also, I started working on a D-Bus API for KWin. The API will expose most of libinput configuration settings. Currently it lists all available devices, some of their most important read-only properties (like name, hardware ids, capabilities), and allows to enable/disable tap-to-click as an example of writable property. As I already said, KCM isn't yet ready, but I was able to enable tap-to-click on my touchpad using qdbusviewer.

My kwin repo clone [is here](http://quickgit.kde.org/?p=clones%2Fkwin%2Falexandermezin%2Fkwin.git), branch libinput-dbusconfig
