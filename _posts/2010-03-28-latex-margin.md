---
layout: post
title: "[latex] 調邊界留白 (margin) 的方法"
date: '2010-03-28T09:45:00.000+08:00'
author: mjtsai
tags: latex
modified_time: '2010-04-04T21:59:27.133+08:00'
blogger_id: tag:blogger.com,1999:blog-6729751024593483406.post-5494859101423122121
blogger_orig_url: https://mongala-memo.blogspot.com/2010/03/latex-margin.html
---

-- 2004/06/29 bbs backup --


{% highlight plaintext %}
※ 本文轉錄自 [TeX] 看板

發信人: Kang-min Liu , 看板: TeX
標  題: [FYI] 調邊界留白 (margin) 的方法
發信站: SEEDNet News Service (Tue Oct 14 19:22:14 2003)
轉信站: wretch!netnews.csie.nctu!news.ee.ttu!news.cis.nctu!freebsd.ntu!news.ntu
Origin: 203.70.26.97


本來 latex 排出來的文件，上下左右留白的空間都很大
在 \begin{document} 之前加上以下幾行
就可以多用一些空白

\oddsidemargin  0.0in
\headheight     0.0in
\topmargin      0.0in
\evensidemargin 0.0in
\textheight     9.0in
\textwidth      6.5in

要注意的是，其實並不是在調 margin , 而是用 textheight 與 textwidth
在調中間文字的最大區域，不妨自已多試幾種好用的組合。

Cheers,
Kang-min Liu
{% endhighlight %}

