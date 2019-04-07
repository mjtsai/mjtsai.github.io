---
layout: post
title: 1st time play raspberry pi
date: '2013-03-04T00:29:00.000+08:00'
author: mjtsai
tags: 
modified_time: '2013-03-17T21:14:49.477+08:00'
thumbnail: http://3.bp.blogspot.com/-Y1KHNMR_-sk/UTNY3L51ZTI/AAAAAAAALvA/jQQnAl-eauE/s72-c/16984_3875024848886_99609985_n.jpg
blogger_id: tag:blogger.com,1999:blog-6729751024593483406.post-1427465038071900202
blogger_orig_url: https://mongala-memo.blogspot.com/2013/03/1st-time-play-raspberry-pi.html
---


Many people playing the tiny board and many communities supporting it, so I bought one to be a media center and wireless AP(and further applications next).

It's easy to install raspbmc on the sd card without any command for settings. It can be controlled by the CEC supported TV. I don't have to link to an IR sensor and buy a remote controller.

![fig1](https://drive.google.com/uc?id=19rXmf6fr-3D_08h7ZNsfpP2zmDG6pvqk)

![fig2](https://drive.google.com/uc?id=1-4JovLnI2uGRkguWyF0sCBaUEtn4MKTY)

Smoothly it plays the video with the HW decoder. Some codec, MPEG, VC1, you have to buy. Some codec, RM, RMVB... , it does not support. I'll find out if it can run with external players and overclocking.

![fig3](https://drive.google.com/uc?id=1fbBP-aZdUJaif0jBxl7VC5gC8LwJXMjQ)

~~Unfortunately I cannot play YOUTUBE on raspbmc~~(now I can)... so install xbian instead. Defaultly it is overclocking to 840Mhz to get better performance but hotter. Take the config in `/boot/config.txt`.


Can be controlled with "XBMC official remote" app on iphone in the same net domain. You should turn on this feature in XBMC.

![fig4](https://drive.google.com/uc?id=10ZCnRbF4Z6GYjce3nTZd7fd56gGMBxVF)


Turn on AirPlay and try the wifi display.

![fig5](https://drive.google.com/uc?id=1lC_nNTgbaWvtkVe2C_kdh-a5swTNKk6k)
![fig6](https://drive.google.com/uc?id=1EdflHiO6CHt15ejX6C5VjzfyW5CsZ7b5)


It seems playing image is ok but playing video is usually buffering. ~~I don't know why local network speed is not enough.~~ To set connection to 802.11n is more faster.

![fig7](https://drive.google.com/uc?id=1ADr8WiqAiPgknIHPHGK7veSAp_WsHGzC)


Youtube is ok

![fig8](https://drive.google.com/uc?id=1PqqbrwPFRbGeRukt7WwJ8sc-noP779u0)

It can search Chinese with APP keyboard but screen keyboard in native input field. I searched "甄嬛傳".

![fig9](https://drive.google.com/uc?id=1k0FSkv4rpKQxMW57x5ioEfj86B6q49Hs)

Install the [https://code.google.com/p/xbmc-addons-chinese/](https://code.google.com/p/xbmc-addons-chinese/) for China streaming services and keyboard.


![fig10](https://drive.google.com/uc?id=1l9LKgkF4UD6NI5JPdIaLb4lOCbwm8MMn)



Refer to [http://bbs.htpc1.com/thread-142703-1-4.html](http://bbs.htpc1.com/thread-142703-1-4.html), you have to add some codes in the `<addon path>/addon.xml` ，it works on LeTV. I searched "三國" with screen keyboard, but youtube still use the native keyboard and I don't know how the config it(need more time).

By the way, I update the keyboard to the latest r364 on svn. Thanks to the experts.

![fig11](https://drive.google.com/uc?id=1uHTKbjOMsetMON7ci_O6GspKmY-9-U9c)


---

Talk about the AP, I surveyed the compatible and tiny wifi adapter, netis WF2120, with 8188cu chipset supporting soft AP function. It enabled out-of-the-box on xbian with 8192cu driver. (but I compiled another driver from netis web site)

![fig12](https://drive.google.com/uc?id=1IvHQ6j1iastwNDh7rLRNDTCLL7JENyFG)

Follow [http://www.rpiblog.com/2012/12/turn-raspberry-pi-into-wireless-access.html](http://www.rpiblog.com/2012/12/turn-raspberry-pi-into-wireless-access.html) to setup the wifi interface and dhcpd.

But there is one thing to be taken care of, the hostapd. Due to the chipset, in [http://www.raspberrypi.org/phpBB3/viewtopic.php?p=270652](http://www.raspberrypi.org/phpBB3/viewtopic.php?p=270652), `driver=nl80211` must be replaced with `driver=rtl871xdrv` in `/etc/hostapd/hostapd.conf` and replace the execution file with [http://dl.dropbox.com/u/1663660/hostapd/hostapd](http://dl.dropbox.com/u/1663660/hostapd/hostapd) (or recompile by yourself).

Afterward, NEVER config net on XBMC UI or it may overwrite the settings for your AP.



Have fun ~  
(now re-installing because it ~~crashes again~~ haha)  
~~using raspbmc config is more stable.~~

Finally , it seems the problem of power adapter. With iphone power adapter, it's very stable. I'll buy another one.




