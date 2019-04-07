---
layout: post
title: "[latex] Chinese"
date: '2010-03-28T14:14:00.000+08:00'
author: mjtsai
tags: latex
modified_time: '2010-04-11T22:32:46.998+08:00'
blogger_id: tag:blogger.com,1999:blog-6729751024593483406.post-5520096888364442255
blogger_orig_url: https://mongala-memo.blogspot.com/2010/03/latex.html
---

-- 2010 --
Now I love to just download fonts from here cwTeX Unicode Type 1 and copy the fonts to the directory described in section 4.1.2 of the 1st link below. It easy! Under CJK package it works. I usually embed cwmu and cwku. They are enough for my purpose. 
 
-- 2005/02/02 bbs backup -- 
如果是抓果正兄做的王漢宗 type1 字型的話
~~http://info.sayya.org/~edt1023/tex/mycjk/n中文中文ode5.html~~
參考這個    把資料夾弄到指定目錄即可
再參考這個
~~http://neural.ee.ncku.edu.tw/~ccy0927/blog/archives/000179.html~~
路徑要改

如果要內嵌字形
miktex 要改這個
~~http://project.ktug.or.kr/dvipdfmx/~~
不內嵌字型可避免字型授權問題


type1 測試可以 抓人家做好的就可以了



windows 的 MikTeX

`ttf2tfm <字型名稱> -P 3 -E 4` <- 數字不對會有提示 `fontalias@UBig5@...`enter

把產生出來的`tfm`檔拷到 `texmf/fonts` 裡面

把最後一行
`fontalias@UBig5@      Pid = 3 Eid = 4`
複製到  `texmf/ttf2tfm/base/ttfonts.map` 裡面

找到 `texmf/tex/latex/CJK/Bg5`
隨便把一個`c00xxxxxxx.fd`檔打開
把檔名及`fontalias`改成剛剛做的`fontalias` 另存為 `c00fontalias.fd`

執行 `texhash`

文件內要這樣寫
{% highlight latex %}
\begin{CJK}{Bg5}{fontalias}
...
\end{CJK}
{% endhighlight %}
測試王漢宗細明體成功
這樣就不用裝 cwTeX 了



