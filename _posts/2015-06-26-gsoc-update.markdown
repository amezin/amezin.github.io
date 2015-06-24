---
layout: post
title: "Pointing devices KCM: status update"
date: 2015-06-26 11:32:45
categories: kde gsoc
---

For general information about the project, look at [this post]({% post_url 2015-06-16-gsoc-intro %})

Last week I was working mostly on architecture.

There will be 3 modules:

- A library that performs 'dirty work' of talking with X server/Wayland compositor
- A daemon that applies settings on startup and when devices are plugged in
- KCM

# The library

The library is partially implemented already.

For X11 the library consists of 3 layers:

- QObject wrapper for XInput (XInputDevice, XInputDeviceManager)
- Adapters that map XInput objects to the common interface (XInputDeviceAdapter, XInputDeviceManagerAdapter)
- Interface classes (InputDevice, InputDeviceManager)

With code organized in such way it is clear how XInput properties are mapped to properties in the library interface, and the mapping code looks very simple.

For Wayland/KWin/libinput thigs are a bit more complex:

- There will be a module for KWin, that configures libinput inside KWin process
- The module will have a D-Bus interface
- There will be two D-Bus adapter classes, similar to adapters for XInput

Currently I am working on X11 only. I'll start adding Wayland support later, at least when I'll get a working KCM on X11.

# The daemon

The daemon will be a KDED module. The only function that the daemon will support is applying configuration from configuration file. Daemon will apply the configuration automatically when a device is plugged in, and there will be a D-Bus API to trigger it manually.

# KCM

KCM will be, basically, an editor for daemon config. Currently I have a dummy KCM that only shows a list of available devices. I plan to add few configuration options in following days.

# Overall status

I'm still behind schedule, but, I think, I made big progress. The hardest part was getting QML KCM to work.

Kcmshell and systemsettings print misleading error message:

    Error loading plugin "kcm_pointingdevices" "The shared library was not found." 
    Plugin search paths are ("/usr/lib/qt/plugins", "/usr/bin")

However, the KCM loads correctly. I spend a lot of time trying to fix it, but looks like this message is printed as a part of normal execution, and doesn't indicate any actual error.

As I'm starting to work on UI, I'd like to hear what you like/don't like in current Touchpad KCM and Mouse KCM.

As usual, [here is a link to the repository](http://quickgit.kde.org/?p=scratch%2Falexandermezin%2Fpointing-devices-kcm.git).
