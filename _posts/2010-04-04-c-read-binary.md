---
layout: post
title: "[c++] read binary"
date: '2010-04-04T22:28:00.000+08:00'
author: mjtsai
tags: program
modified_time: '2010-04-04T22:28:54.458+08:00'
blogger_id: tag:blogger.com,1999:blog-6729751024593483406.post-1691347115559794297
blogger_orig_url: https://mongala-memo.blogspot.com/2010/04/c-read-binary.html
---


-- 2007/06/19 bbs backup --
<!--more-->

suppose there're codes

{% highlight c++ %}
while(!foo.eof()){
    foo.getline(buf, num);
    // do someting
}
{% endhighlight %}

it works  
but binary maybe take this style or it read more once


{% highlight c++ %}
foo.read(buf, size);
while(!foo.eof()){
    // do something
    foo.read(buf, size);
}
{% endhighlight %}


~~http://www.programmersheaven.com/mb/CandCPP/210340/210340/readmessage.aspx~~
On the last read cycle you still have a valid read, so `eof()` hasn't been reached until you try and read past the last item. Try swapping your code around slightly like in red above, it should work.

