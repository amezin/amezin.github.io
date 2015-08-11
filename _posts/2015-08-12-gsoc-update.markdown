---
layout: post
title: "Pointing devices KCM: status report"
date: 2015-08-12 04:00:00
categories: kde gsoc
---

For general information about the project, look at [this post]({% post_url 2015-06-16-gsoc-intro %})

I didn't post any updates for a long time, mostly because I was coding actively, and completely forgot about anything else :)

First of all, new screenshots:

![KCM - Mouse settings](/images/kcm-newlayout-mouse.png)

![KCM - Touchpad settings](/images/kcm-newlayout-touchpad.png)

# Current status #

On X11:

- All properties of libinput driver can be configured from UI.

- Incomplete UI for evdev and synaptics drivers.

On Wayland:

- Works with patched KWin.

- Uses the same UI as on X11 (libinput).

# Near-term plans #

- Refactoring.

- Write more tests.

- UI improvements for libinput - adjust layout, better names for some options, add tooltips.

- Also, I'll try to get rid of 'Device' combo box. It would be cool if every device is displayed as a separate KCM. However, currently I have no idea how to achieve it.

# Long-term plans (post-GSoC) #

- Implement button mapping configuration on X11. It is necessary for evdev driver to enable left-handed mode, and isn't available as XInput property.

- Finish UI for evdev and synaptics.

- Probably, I will port automatic disable logic from Touchpad KDED module. Only libinput has built-in automatic disable. However, as libinput becomes more widespread, there will be no need for custom implementation.

# How to try #

- You can get the source from `git://anongit.kde.org/scratch/alexandermezin/pointing-devices-kcm.git`

- There is a [packaging script for Arch Linux in AUR](https://aur.archlinux.org/packages/kcm-pointing-devices-git/)

Beware! It crashes with latest stable libxcb and xcb-proto. To make it work you will need xcb and xcb-proto from git.

## Kwin/Wayland ##

Wayland support isn't enabled by default, and I doubt anybody wants to try it today :) But if you want, you need to:

- Build KWin from my repo: `git://anongit.kde.org/clones/kwin/alexandermezin/kwin.git` (branch libinput-dbusconfig).

- Pass `-DBUILD_KWIN_BACKEND=ON` to cmake.
