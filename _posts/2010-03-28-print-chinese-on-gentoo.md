---
layout: post
title: print chinese on gentoo
date: '2010-03-28T10:44:00.000+08:00'
author: mjtsai
tags: unix
modified_time: '2010-03-28T10:44:02.665+08:00'
blogger_id: tag:blogger.com,1999:blog-6729751024593483406.post-3538435971410080751
blogger_orig_url: https://mongala-memo.blogspot.com/2010/03/print-chinese-on-gentoo.html
---


-- 2004/08/03 bbs backup -- 
ghostscript:
<!--more-->

~~http://netlab.cse.yzu.edu.tw/~statue/freebsd/zh-tut/print.html#NOW-PRINTING~~

記得字型的路徑要正確  
不然找不到

bsd放在`/usr/local/share...`下  
但是gentoo放在`/usr/share`

`CIDMap`??  
其實是`CIDMap.CJK`要改  
forgot....wait


### mozilla:

#### add some feature to `about:config`:

{% highlight javascript %}
user_pref("print.postscript.nativecode.zh-TW", "big5");
user_pref("print.postscript.nativefont.zh-TW", "MSung-Light-B5-H");
{% endhighlight %}

it's an example...

呃 這是寫在 `pref.js` 裡面的
如果在 `about:config` 就直接加 key 和值就好了


#### replace the print command:

{% highlight shell %}
    gs -q -sDEVICE=pswrite "-sOutputFile=/tmp/out.ps"
"-dNOPAUSE -dBATCH -dSAFER" &&
lpr ${MOZ_PRINTER_NAME:+'-P'}${MOZ_PRINTER_NAME}
/tmp/out.ps && rm -f "/tmp/out.ps"
{% endhighlight %}

接成一行  
mozilla 一開始是直接去呼叫 lpr 列印
什麼指令之類的並不支援中文
所以要先用 gs 轉成中文後再印
所以在印之前可以先印成檔案看看可不可以用中文



聽說 OOO 可以用他的方式印中文
那再來要解決的就是 gvim 了

不過要換字型的話還是要對 ghostscript 的配置多了解些才行


