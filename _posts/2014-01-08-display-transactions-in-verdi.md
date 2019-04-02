---
layout: post
title: 'display transactions in Verdi'
date: 2014-01-08 13:44
comments: true
categories: [verification]
---

REF:
[Linking Novas Files With Simulators and Enabling FSDB Dumping](http://zh.scribd.com/doc/63500618/Linking-Novas-Files-With-Simulators-and-Enabling-FSDB-Dumping)
[Transaction Level Debug with SystemVerilog VMM & Verdi](http://www.slideshare.net/svenka3/transaction-level-debug-with-systemverilog-vmm-verdi)
[1]:http://zh.scribd.com/doc/63500618/Linking-Novas-Files-With-Simulators-and-Enabling-FSDB-Dumping

Most of these years I verified serial interfaces. It was difficult to identify the meaningful data of serial interfaces in waveform of signal level(I always thought I was decoding Morse Code by hand). What I needed was a graphical representation to decode the collection of signals to higher level and meaningful information, the transaction. I found Verdi has the function, but I need add some code in my program.

<!--more-->

This is an old function. The syntax is - 
`$fsdbLog(["label"], ["message"], [severity], ["stream_name"][, variable |"string"]* );`

The [1st link][1] has more description in detail, but in my words:

- label               : what display on the title bar of each transaction boxes, e.g. MSC\_PKT below
- message             : display in the 1st line inside transaction boxes if set
- serverity           : the same meaning in general and display in the line below message
- stream\_name         : the name on the left bar equivalent to signal name of DUT
- variable | "string" : the content inside the transaction boxes below serverity, e.g. MSC\_PKT DATA ...

![transactions](https://lh4.googleusercontent.com/-XBcm6KKDD2Q/Us1W_7AFRyI/AAAAAAAAMKc/Wmalv6cNtzw/w1276-h416-no/haha.png)
