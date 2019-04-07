---
layout: post
title: "[latex] save utf8 file"
date: '2010-03-28T17:50:00.000+08:00'
author: mjtsai
tags: latex
modified_time: '2010-04-11T22:54:38.546+08:00'
blogger_id: tag:blogger.com,1999:blog-6729751024593483406.post-1551820480844123647
blogger_orig_url: https://mongala-memo.blogspot.com/2010/03/latex-utf8-save-file.html
---


--2010--
Now I use vim. Vim does not add BOM in files.

<!--more-->

--2005/09/27 bbs backup --

檔頭有問題要儲存成
utf8 without BOM

[http://www.javaworld.com.tw/jute/post/view?bid=29&id=105449&sty=1&tpg=1&age=0](http://www.javaworld.com.tw/jute/post/view?bid=29&id=105449&sty=1&tpg=1&age=0)  
在檔案開首, 其實加入了數 bytes 的資料來定義那是什麼的編碼, 稱為 Byte Order Mark, BOM (由 unicode.org 制定的嗎?).

{% highlight plaintext %}
EF BB BF: UTF-8
FE FF: UTF-16/UCS-2, little endian
FF FE: UTF-16/UCS-2, big endian
FF FE 00 00: UTF-32/UCS-4, little endian.
00 00 FE FF: UTF-32/UCS-4, big-endian.
{% endhighlight %}
