---
layout: post
title: "[latex] ghostscript"
date: '2010-04-04T21:57:00.000+08:00'
author: mjtsai
tags: latex
modified_time: '2010-04-04T21:57:25.555+08:00'
blogger_id: tag:blogger.com,1999:blog-6729751024593483406.post-6878923807478222157
blogger_orig_url: https://mongala-memo.blogspot.com/2010/04/latex-ghostscript.html
---


-- 2006/10/27 bbs backup --
<!--more-->

升級升過頭
導致原本 miktex 的 ghostscript 沒辦法轉換成 pdf  
似乎抓不到字型



經過修正   
把`/dvipdfm/config/dvipdfmx.cfg`裡的   

{% highlight shell %}
D  "mgs.exe -q -dNOPAUSE -dBATCH -sPAPERSIZE=a0 -sDEVICE=pdfwrite
-dCompatibilityLevel=1.3 -dAutoFilterGrayImages=false
-dGrayImageFilter=/FlateEncode -dAutoFilterColorImages=false
-dColorImageFilter=/FlateEncode -dUseFlateCompression=true
-sOutputFile=\"%o\" \"%i\" -c quit"
{% endhighlight %}

改成

{% highlight shell %}
D  "gswin32c -q -dNOPAUSE -dBATCH -sPAPERSIZE=a0 -sDEVICE=pdfwrite
-dCompatibilityLevel=1.3 -dAutoFilterGrayImages=false
-dGrayImageFilter=/FlateEncode -dAutoFilterColorImages=false
-dColorImageFilter=/FlateEncode -dUseFlateCompression=true -sOutputFile=%o %i
-c quit"
{% endhighlight %}


也就是不要用 miktex 內附的 ghostscript 用系統的 ghostscript   
反正我本來就有裝   
這樣就可以解決轉檔的問題

