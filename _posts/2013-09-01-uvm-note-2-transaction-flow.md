---
layout: post
title: 'UVM note - (2) transaction flow - send transaction'
date: 2013-09-01 12:22
comments: true
categories: [uvm, verification]
---
依照參考架構接出來的環境會盡量使用 uvm lib 已經有的元件，因此了解 transaction flow 是必要的，才知道如何套用、修改，在 uvm_user_guide 內有張圖大致描述了 transaction flow ，不過我還是覺得 trace code 比較準一些，參考流程使用的 macro ，其實都可以拆開成基本的 funciton call，視環境需要再作組合。  
Components of uvm lib is applied as much as possible in reference architecture so understanding the transaction flow is necessary. There is a diagram to briefly describe the transaction flow in the uvm_user_guide, however, less precise than tracing code in my opinion. Besides the basic functions inside the macro of the reference flow can be re-assembled depends on requirement of verification environment.

<!--more-->
uvm_user_guide#.pdf
![flow.png](http://user-image.logdown.io/user/838/blog/831/post/98731/yFhuPL6rRkeTqsgsaAyv_flow.png)

舉個例子，通常參考 flow 用 `` `uvm_do `` 去呼叫 sequence，但其實註解內就說明了有三種方法可以呼叫。  
For example, usually it uses `` `uvm_do`` to enable sequence in reference flow, but in the code there are 3 ways to enable the sequence.

In uvm_sequence_base.svh, there are 3 ways to create sequence.
1. call `start`
2. call `start_item` and `finish_item`
3. call `` `uvm_do_*``

{% highlight verilog %}
	// CLASS: uvm_sequence_base
	//
	// The uvm_sequence_base class provides the interfaces needed to create streams
	// of sequence items and/or other sequences.
	//
	// A sequence is executed by calling its <start> method, either directly
	// or indirectly via <start_item>/<finish_item> or invocation of any of
	// the `uvm_do_* macros.
{% endhighlight %}  
  
畫了一張 trace code 的流程圖，以最基本的呼叫方式，以後再看會比較清楚些，不過這邊沒有處理回傳 sequence item 的流程。  
There is a sequence diagram created by tracing code for further use following basic function calls, excluding the flow of returning sequence item. 

ps. beware of `start` calls `pre_body()` but `finish_item` and `uvm_do_*` don't

![uvm_transaction_transmit.svg](https://drive.google.com/uc?id=0Bxm9QxsD8PDPRFhJV29PbmxkY0U)
