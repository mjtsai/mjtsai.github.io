---
layout: post
title: "[latex] bibtex"
date: '2010-03-28T18:39:00.001+08:00'
author: mjtsai
tags: latex
modified_time: '2010-04-11T23:14:15.509+08:00'
blogger_id: tag:blogger.com,1999:blog-6729751024593483406.post-7731899941311945002
blogger_orig_url: https://mongala-memo.blogspot.com/2010/03/latex-bibtex.html
---

> -- 2010 --

How the citation be displayed depends on the bibliography style. I suggest to save author's full name in the file. It may display the acronym if the style assigns. We don't spend too much effort on it.

> -- 2005/10/26 bbs backup -- 

為了要引入參考資料而設計的工具

<!--more-->

建一個xxx.bib檔，內容如下:

{% highlight latex %}
@article{ TH,    ---->  key
title="A New Approach for the Extraction of Threshold Voltage for MOSFET's",
author="{Jen Shuang Wong, Jian Guo Ma, Kiat Seng Yeo, Manh Anh Do}",
year=" ",
pages="4",
}
@book{
    items....
}
{% endhighlight %}

在本文中:

加在要告知參考的地方
{% highlight latex %}
\cite{}
{% endhighlight %}

這是條列出所有的參考資料
{% highlight latex %}
\bibliographystyle{your style}
{% endhighlight %}

{% highlight latex %}
\bibliography{your bib file}
{% endhighlight %}

