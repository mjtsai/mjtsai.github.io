---
layout: post
title: "[latex] ieeetran citation"
date: '2010-04-04T23:17:00.000+08:00'
author: mjtsai
tags: latex
modified_time: '2010-04-16T00:12:13.448+08:00'
blogger_id: tag:blogger.com,1999:blog-6729751024593483406.post-3775007547894948361
blogger_orig_url: https://mongala-memo.blogspot.com/2010/04/latex-ieeetran-citation.html
---


-- 2010 --
I expect it shows `[1-10]` for 10 continuous citations but `[1]-[10]` instead. I cannot find any solution for it until I give up then try to trace codes in `IEEEtrans.cls`.
<!--more-->



I've found the definition `\def\citedash{]--[}` and guessed it is the format. After redefine the pattern , `\renewcommand\citedash{--}`, the `[1-10]` pattern shows. 

-- 2008/07/19 bbs backup --

因為 cite 連續的 reference，
原本預期會編成這樣

{% highlight plaintext %}
[1-10]
{% endhighlight %}

但編出來的結果是，

{% highlight plaintext %}
[1]-[10]
{% endhighlight %}



一直找不到有人也有同樣的問題，經由 trace code 得知，原本定義在 `IEEEtran.cls` 裡面的

{% highlight latex %}
\def\citedash{]--[}
{% endhighlight %}


是那個樣式的定義，因此重新定義此樣式，

{% highlight latex %}
\renewcommand\citedash{--}
{% endhighlight %}

這樣就可排出 `[1-10]` 的效果
