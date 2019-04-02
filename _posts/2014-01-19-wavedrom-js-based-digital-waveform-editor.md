---
layout: post
title: 'wavedrom - 基於 js 的 digital waveform 編輯器'
date: 2014-01-19 16:16
comments: true
categories: 
---
### Website
[http://wavedrom.com/](http://wavedrom.com/)
~~[https://code.google.com/p/wavedrom/](https://code.google.com/p/wavedrom/)~~
<!--more-->
### Online Editor
[http://wavedrom.com/editor.html](http://wavedrom.com/editor.html)
~~[http://wavedrom.googlecode.com/svn/trunk/editor.html](http://wavedrom.googlecode.com/svn/trunk/editor.html)~~
### Document
[http://wavedrom.com/tutorial.html](http://wavedrom.com/tutorial.html)
~~[http://wavedrom.googlecode.com/svn/trunk/tutorial.html](http://wavedrom.googlecode.com/svn/trunk/tutorial.html)~~
### Example
<script src="https://gist.github.com/asolkar/2878346.js"></script>
![axi](https://lh6.googleusercontent.com/-QmgXgE1KkOk/Uu9zR0gpS1I/AAAAAAAAMLk/WdZIr0bEM6s/w795-h233-no/axi.png)
------

## First Meet

公司的 designer 有使用 excel 的外掛來畫 waveform ，似乎是前人開發的，不過我覺得圖片不好看而且被綁在 M$ 上，因此一直在尋找 open source 圖樣又漂亮的工具，最好是 web 版的，這樣我以後可以架站整合一些工具。於是被我找到了 wavedrom ，他是用 js 寫的，剛好滿足我的需求，描述式則是很簡單的 WaveJSON。

## WaveJSON
[https://github.com/drom/wavedrom/wiki/WaveJSON](https://github.com/drom/wavedrom/wiki/WaveJSON)
~~[https://code.google.com/p/wavedrom/wiki/WaveJSON](https://code.google.com/p/wavedrom/wiki/WaveJSON)~~

WaveJSON 基於 JSON ，但是保留了一些關鍵字作為識別，猜測程式是抓到格式之後去找 [https://github.com/drom/wavedrom/wiki/WaveDromSkin](https://github.com/drom/wavedrom/wiki/WaveDromSkin)  ~~[https://code.google.com/p/wavedrom/wiki/WaveDromSkin](https://code.google.com/p/wavedrom/wiki/WaveDromSkin)~~ 裡面的圖片部件拼成描述的樣子。他支援了
- 0, 1
- pull-up, pull-down
- x, z
- bus
- clock

基本上夠用了。不過我可能還需要虛線的圖形，目前只有 pull-up、pull-down 有虛線；另外圖形基本上都要對齊 clock，但我有不對齊 clock 的需求，目前的解法暫時是把 clock 的單位畫長一點（用period），訊號transition 就可以不用對齊 clock。



## Embeded in html5 slide

在完成了 html5 的投影片之後再看到 wavedrom ，第一時間就是想說能不能嵌入投影片，果然，這個問題已經被討論過了，~~[https://wavedrom.googlecode.com/svn/trunk/impress.html#/s1](https://wavedrom.googlecode.com/svn/trunk/impress.html#/s1)~~ [http://wavedrom.com/impress.html#/s1](http://wavedrom.com/impress.html#/s1)有範例。

The first I think while finding wavedrom after completing html5 slide is if it can be embeded in the slide. As expected, the issue has been discussed, e.g. ~~[https://wavedrom.googlecode.com/svn/trunk/impress.html#/s1](https://wavedrom.googlecode.com/svn/trunk/impress.html#/s1)~~

ps. html5 投影片也可以整合 mathjax ~~[http://naoyat.github.io/slides/memo/html5slides+MathJax.html#1](http://naoyat.github.io/slides/memo/html5slides+MathJax.html#1)~~
ps. mathjax also can be embeded in html5 slides ~~[http://naoyat.github.io/slides/memo/html5slides+MathJax.html#1](http://naoyat.github.io/slides/memo/html5slides+MathJax.html#1)~~









