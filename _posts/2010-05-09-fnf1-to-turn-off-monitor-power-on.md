---
layout: post
title: fn+f1 to turn off monitor power on thinkpad
date: '2010-05-09T15:10:00.001+08:00'
author: mjtsai
tags: unix
modified_time: '2010-05-09T15:41:20.710+08:00'
blogger_id: tag:blogger.com,1999:blog-6729751024593483406.post-8477355981841892746
blogger_orig_url: https://mongala-memo.blogspot.com/2010/05/fnf1-to-turn-off-monitor-power-on.html
---


ubuntu 10.04

It's based on acpid, acpi-support. while some hotkeys pressed, acpi events are triggered then some handlers be called according to the events respectively. 

`/etc/acpi` contains scripts for handler, `/etc/acpi/events` contains the events definition. Now it targets on turn off monitor power because it has to modify some codes in my laptop. Fn+F1 is the hotkey to turn off monitor power.

The `screenblank.sh` is the handler. It finally calls `xset dpms force off` to turn off monitor power, but before the command becomes effective, it detects some user information. It fails in 3 lines of the file: 

{% highlight shell %}
for x in /tmp/.X11-unix/*; do
    displaynum=\`echo $x | sed s#/tmp/.X11-unix/X##\`
    getXuser;
{% endhighlight %}

because there is no `/tmp/.X11-unix folder` in my laptop. Subsequently, `getXuser` is called from `/usr/share/acpi-support/power-funcs` and it finds the pattern of `:$displaynum`. However, there is no colon in the results of command `finger` so it finds nothing.


In the workaround solution, `$displaynum` is forced to `0` and ``user=`finger| grep -m1 ":$displaynum " | awk '{print $1}'` `` is modified to ``user=`finger| grep -m1 tty | awk '{print $1}'` `` in the code of `getXuser` function copied from power-funcs and pasted in `screenblank.sh`. No code be removed and it can be reverted to the original codes.

