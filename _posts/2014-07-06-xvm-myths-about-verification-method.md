---
layout: post
title: 'xVM 的迷思   關於 verification 方法'
date: 2014-07-06 14:12
comments: true
categories: [verification]
---
~~脫離了 verification 界~~，先來做一下小小心得總結

xVM = UVM, OVM, VMM ...

Methodology 這件事情，實在是太抽象了以至於我是從實做中體會其意義，大概就是設計一套流程，用來得到想得到的數據，必須是好操作或者是自動化。對於 verfication 來說，我覺得重點就是 1. 如何確認 HW 在特定 pattern 的正確性 2. 所有 pattern 的 coverage 夠不夠高 3. pattern 是否集中在合乎應用的狀況，有沒有 over-test 的問題。跟要用哪套其實沒有很大的相關性，黑貓白貓，可以抓老鼠的就是好貓。
<!--more-->

從去年到今年，verification 的缺突然多很多，然後很多都要會 xVM ，雖然我不知道為何突然需要，對我來說，xVM 其實沒有好到非要不可，唯一比較強勢的就是他們是標準，lib 又滿充足，交換比較方便。這種 constraint random 的模式，還是要看應用才能使用其好處。

簡單分類一下

1. 純 constraint random 可以解決的，我覺得是傳輸類(communication)的 module。我的定義是 input to output 過程中 data 會被分解或重組，但是內容不變，如果有些計算，也是很簡單的計算，像是 CRC。

	例如：AXI, USB, HDMI ... 等

	這些的測法就拿組合好的 output 和 input 比就可以了，直接 toggle 訊號。

2. 需要 reference model 或 reference dump 才能解決的，我覺得是計算類(computation)的 module。我的定義是 input to output 過程中 data 的內容會改變。有時候還需要搭配 SW 一起。

	例如：DSP, image processing, h264 codec ... 等

	要用 systemverilog 刻一個 model 是很困難的而且很慢，用 constraint random 的方式也會常常填到不合法的值，硬要用的話 constraint 很難寫，最近終於問到了一致的想法，看來實務上別人也這樣覺得，除了 xVM 勢必要搭配其他的方法才適合。
  
3. formal ，實務上倒是沒使用過，上面都是 simulation based 的方式，如果結構簡單但 simulation effort 太大的可以考慮 formal ，聽別人說的。



