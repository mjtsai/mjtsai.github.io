---
layout: post
title: necessary components for uvm in my opinion
date: '2013-04-16T00:33:00.001+08:00'
author: mjtsai
tags: 
modified_time: '2013-04-16T00:33:19.026+08:00'
thumbnail: http://2.bp.blogspot.com/-k_Nqy2eIM2w/UWwmAlZOmLI/AAAAAAAALy8/WM3-tloRNA4/s72-c/Diagram1.png
blogger_id: tag:blogger.com,1999:blog-6729751024593483406.post-1276641849602842678
blogger_orig_url: https://mongala-memo.blogspot.com/2013/04/necessary-components-for-uvm-in-my.html
---


我覺得使用uvm需要有這些必要元素，interface 作為test class和dut的接口，可是要在module內先造出instance，很有趣的是如果拿function 去收硬體訊號，則只會在call function 時latch 一次而已，在function 內重抓也不會更新，但interface 可以讓class內一直更新硬體訊號；class以上都當作軟體；而整個模擬的切入點則來自`run_test`，要有個program 或module 去call `run_test`，整個模擬就會開始了

![fig1](https://drive.google.com/uc?id=1hc0mVWgxq0v87stCP1L6NgOZJgqL_DWt)
