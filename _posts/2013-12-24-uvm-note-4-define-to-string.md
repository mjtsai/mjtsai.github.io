---
layout: post
title: 'UVM note - (4) `define to string'
date: 2013-12-24 15:54
comments: true
categories: [uvm, verification]
---
今天在串 uvm RAL built-in test 時遇到一個問題，就是處理 backdoor 時需要設定 *hdl_path*，也就是 `set_hdl_path()`，要傳入字串，但環境已經有 define 一些 hierarchy 了，如果不能利用既有的 define 而要重新從 top 開始寫，就浪費既有的資源，還好 stackoverflow 已經有解了，利用 `` `"x`" `` 就可以把 define 換成 字串，非常實用的技巧。

I got a problem while building uvm RAL built-in test, which is passing *hdl_path* string into the function `set_hdl_path()` to enable backdoor function. However there are some hierarchy defines' in the environment. It is worthless to rewrite the string from top without applying the existing defines'. Luckily, there is the solution in stackoverflow by using `` `"x`" `` to transfer `define to string. Very useful trick.


REF : [How to create a string from a pre-processor macro](http://stackoverflow.com/questions/15373113/how-to-create-a-string-from-a-pre-processor-macro)