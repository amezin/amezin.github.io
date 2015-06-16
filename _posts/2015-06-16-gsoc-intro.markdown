---
layout: post
title: "GSOC: new unified KCM for mouse and touchpad"
date: 2015-06-16 17:27:45
categories: kde gsoc
---

This year I'm participating in Google Summer of Code with a project called "Pointing Devices KCM". It is about creating new unified KCM for both mouses and touchpads (and maybe some other devices like ThinkPad's pointing stick later).

Why new KCM?

- Mouse KCM and Touchpad KCM should have a lot of common code. Both of them change properties of XInput devices (a lot of code, actually). And touchpads and mouses have few common properties. Currently, every KCM implements things its own way.
- Also, I think that Mouse and Touchpad KCMs should have similar UI. Both of them should have the "testing area". Or both of them shouldn't.
- Current mouse KCM controls so-called "master pointer". Changes in it actually affect all pointer devices, including touchpad. Of course, that's not how it is expected to work.
- None of these KCMs can handle multiple devices.
- None of these KCMs can handle Wayland. I planned Wayland support for Touchpad KCM, but it seems that I did too many mistakes. It doesn't look like Wayland support can be added to it easily.

For me it looks like fixing all these problems in existing code will take a lot more time and effort than writing new KCM. And writing something new is always more fun :)

# Current status

Unfortunately, graduating from university took a lot more time than I expected. So I was able to start coding this week only. But now I've finished almost everything and, hopefully, will be able to catch up my original schedule.

I heard Touchpad KCM code looked scary for people who reviewed it. Especially the XInput-related code. So as a first step I decided to implement a nice (to my taste) utility library. Currently it can handle XInput hierarchy and property notifications, enumerates devices and change their properties. There's also few tests for it.

For now I'll be keeping all my code in [this scratch repo](http://quickgit.kde.org/?p=scratch%2Falexandermezin%2Fpointing-devices-kcm.git).

UPD: Looks like xcb_input_xi_change_property is broken in current release of XCB. It triggers assert() for property values that have length not divisible by 4 (bytes). And even git version has this problem too. But there is a [patch available on XCB mailing list](http://lists.freedesktop.org/archives/xcb/2015-June/010385.html) that fixes the problem.
