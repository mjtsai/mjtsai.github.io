---
layout: post
title: "[latex] 調邊界留白 (margin) 的方法"
date: '2010-03-28T09:47:00.000+08:00'
author: mjtsai
tags: latex
modified_time: '2010-04-04T21:59:12.633+08:00'
blogger_id: tag:blogger.com,1999:blog-6729751024593483406.post-3032130261028635294
blogger_orig_url: https://mongala-memo.blogspot.com/2010/03/latex-margin_27.html
---


-- 2004/06/29 bbs backup -- 


{% highlight plaintext %}
※ 本文轉錄自 [TeX] 看板

發信人: hoch.bbs@bbs.cis.nctu.edu.tw (prolactin), 看板: TeX
標  題: Re: [FYI] 調邊界留白 (margin) 的方法
發信站: 交大資科_BBS (Wed Oct 15 13:58:27 2003)
轉信站: wretch!netnews.csie.nctu!freebsd.ntu!news.cis.nctu!cis_nctu
Origin: 202.90.17.4 
以英文來講, 每一行應該排多少字不是隨便決定的. 一般人會覺得 LaTeX
內定的 textwidth 太小. 如果把 \textwidth 設為 9.0in, 以 12pt 的 cmr12
而言, 一行可以長到 88 個字 (characters + spaces + punctuation marks);
11pt 的 cmr11 更會長到 97 個 characters. 這已經遠遠超過一般認為
適當的 66 characters (see, e.g., http://www.ctan.org/tex-archive/macros/latex/contrib/memoir/memman.pdf, page 24)

總而言之, textwidth 必須依照使用的 fontsize 來設定. LaTeX 內定的
是太小沒錯, 我個人覺得 6.5 in 太大了, 尤其是 A4 的紙寬 210mm 比
letter size 的 216mm 還窄.

至於一頁要多少行, 就比較隨便了.原則上和 \baselineskip
有關, 如果你是用所謂的 "single space", 就不太適合很大的
\textheight, 不然一頁太多行看起來太累了.

把 \headheight 設為 0,
本文上面的 headings 就不知道要放那裡了.
{% endhighlight %}

