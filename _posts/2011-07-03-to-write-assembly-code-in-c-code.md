---
layout: post
title: To write assembly code in c code
date: '2011-07-03T02:03:00.000+08:00'
author: mjtsai
tags: program
modified_time: '2011-07-03T02:07:11.049+08:00'
blogger_id: tag:blogger.com,1999:blog-6729751024593483406.post-680967456677273956
blogger_orig_url: https://mongala-memo.blogspot.com/2011/07/to-write-assembly-code-in-c-code.html
---

[http://www.ibiblio.org/gferg/ldp/GCC-Inline-Assembly-HOWTO.html](http://www.ibiblio.org/gferg/ldp/GCC-Inline-Assembly-HOWTO.html)

I need to write some assembly code in c code for embedded system. It's simple if only pure assembly code is needed. Just write op code with registers in a `.s` file. Unfortunately, it has to link variables in c code to assembly code, so I need more advanced knowledge.
<!--more-->


pure assembly for MIPS:

{% highlight c %}
asm volatile("lw t0, (t1)");
{% endhighlight %}

But how do you know the address in `t1` of a variable?

In c code there's a template (sec. 5):

{% highlight c %}
asm ( assembler template 
           : output operands                  /* optional */
           : input operands                   /* optional */
           : list of clobbered registers      /* optional */
           ); 
{% endhighlight %}

The document is very detailed. If there is no operands, just place two consecutive columns. 

{% highlight c %}
int a=10, b;
asm ("movl %1, %%eax; 
      movl %%eax, %0;"
     :"=r"(b)        /* output */
     :"r"(a)         /* input */
     :"%eax"         /* clobbered register */
     );       
{% endhighlight %}

`r` means that compiler selects arbitrary registers to save the variable value and keep it in the register. `=` means it is output value. `%0` means 0th parameter(`b` here) and `%1` means 1st parameter(`a` hear).

{% highlight c %}
asm volatile("lw t0, (t1)"); 
-> 
asm volitile("lw t0, (%0)"::"r" (VAR));

asm volitile("lw %0, (ADDR)":"=r"(VAR));
{% endhighlight %}

