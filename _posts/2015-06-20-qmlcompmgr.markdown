---
layout: post
title: "QML compositing manager for X11"
date: 2015-06-20 7:20:45
---

This post isn't generally related to KDE. But, I think, it might be interesting to the community, especially to developers.

Once upon a time I looked at QtWayland module. QML compositor example, in particular. And decided to build something similar for X11. At first I tried to build a window manager, but the task was too complex. A standalone compositing manager looked like more realistic task.

So, [here is the result](https://github.com/amezin/qmlcompmgr).

It isn't ready for daily use. It crashes from time to time. It has problems with performance because there's almost no optimization. For example, it draws windows that are covered by other windows completely. But in some test cases it outperforms [Compton](https://github.com/chjj/compton) (with glx backend), thanks to Qt Quick's Scene Graph.

And here is a short video showing it in action (with Openbox):

<video preload="metadata" controls>
    <source src="{{ site.baseurl | prepend: site.url }}/video/qmlcompmgr.webm" type="video/webm">
    <source src="{{ site.baseurl | prepend: site.url }}/video/qmlcompmgr.mp4" type="video/mp4">
</video>

Implemented effects:

* Window show/hide animation

* Dim inactive windows (though it dims too many windows)

* Shadows

Known problems:

* Performance

* Only properties of the 'frame window' are inspected. Fixing this will require major changes in source code

* Once it crashed when about 300 windows was mapped in a short period of time

UPD: re-uploaded video in multiple formats, now it should play fine in Chromium
