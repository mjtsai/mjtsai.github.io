---
layout: post
title: "[ARM] coprocessor CP15 - system control coprocessor"
date: '2012-11-18T11:20:00.001+08:00'
author: mjtsai
tags: program
modified_time: '2012-11-26T13:23:06.217+08:00'
blogger_id: tag:blogger.com,1999:blog-6729751024593483406.post-28305379841794113
blogger_orig_url: https://mongala-memo.blogspot.com/2012/11/arm-coprocessor-cp15-system-control.html
---


### Purpose

[Cortex-A8 Technical Reference Manual Revision: r3p2 3.1. About the system control coprocessor](http://infocenter.arm.com/help/index.jsp?topic=/com.arm.doc.ddi0388e/CIHEHDHJ.html)

The purpose of the system control coprocessor, **CP15**, is to control and provide status information for the functions implemented in the processor. The main functions of the system control coprocessor are:
- overall system control and configuration
- cache configuration and management
- Memory Management Unit (MMU) configuration and management
- preloading engine for L2 cache
- system performance monitoring.
<!--more-->


### Instruction
{% highlight armasm %}
mcr{cond} p15, <opcode_1>, <rd>, <CRn>, <CRm>, <opcode_2> 
mrc{cond} p15, <opcode_1>, <rd>, <CRn>, <CRm>, <opcode_2> 
{% endhighlight %}

Following the order, `CRn -> Op1 -> CRm -> Op2`, to look up the entry of target register in manual.


[Cortex-A15 MPCore Technical Reference Manual Revision: r3p2 4.2. Register summary](http://infocenter.arm.com/help/index.jsp?topic=/com.arm.doc.ddi0438g/BABHBIDJ.html)


![table4.1](https://drive.google.com/uc?id=1Nkf2vZtZFwKFMxmH8Xx2cud6sJDTH9ye)




### Catagory


[http://processors.wiki.ti.com/index.php/Cortex-A8_Architecture](http://processors.wiki.ti.com/index.php/Cortex-A8_Architecture)


![a8_arch image](https://drive.google.com/uc?id=10u9VrubrRVBseF1qpDDqNm2SfCMVxAM0)

Example

[Cortex-A15 MPCore Technical Reference Manual Revision: r3p2 4.2.2. c1 registers](http://infocenter.arm.com/help/index.jsp?topic=/com.arm.doc.ddi0438g/CHDGGGIF.html)

![a15 image](https://drive.google.com/uc?id=1MHPuU0vgOdBJMrfcu_xfRnpBfuNktPj-)
....



The mapping is `c1 -> 0 -> c0 ->` to access System Control Register.

{% highlight armasm %}
mcr p15, 0, rX, c1, c0, 0  : write arm to coprocessor , rX -> {c1, 0, c0, 0}
mrc p15, 0, rX, c1, c0, 0  : read coprocessor to arm , {c1, 0, c0, 0} -> rX
{% endhighlight %}

