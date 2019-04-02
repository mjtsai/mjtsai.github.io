---
layout: post
title: 'UVM note - (6) some diff between 1.0p and 1.1 (uvm 不要改 code 好嗎)'
date: 2014-01-04 03:53
comments: true
categories: [uvm, verification]
---
最近嘗試用 uvm 1.1 取代 uvm 1.0p 來跑原本的環境，結果發現有些寫法不能用或是錯誤，想說已經不用 *DEPRECATED* 的部份了怎麼還有問題，trace code 才發現 uvm 1.1 其實滿多地方都有修改，有些不會影響到，有些卻必須要改變原本的寫法，先列兩點，其他遇到再說。  
These days I try to use uvm 1.1 to replace uvm 1.0p, but there are some errors. I don't know why there is problem even if I don't use the *DEPRECATED* part. By tracing code I found there are some code modified. Some have no side effect, but some make me to change code. To list 2 points first.

<!--more-->

1. `start()` of uvm_sequence

![diff of uvm_sequence_base.svh](https://lh6.googleusercontent.com/-52wgR5xgRwM/UseLqWClqkI/AAAAAAAAMG4/dxnSZPBAoO0/w911-h361-no/Screenshot+from+2014-01-04.png)
    
1\.0p 開頭的檢查是   
the check point of 1.0p at beginning
{% highlight verilog %}
if (!(m_sequence_state != CREATED ||
      m_sequence_state != STOPPED ||
      m_sequence_state != FINISHED)) begin
{% endhighlight %}

1\.1 開頭的檢查是    
the check point of 1.1 at beginning

{% highlight verilog %}
if (!(m_sequence_state inside {CREATED,STOPPED,FINISHED})) begin
->
!( m_sequence_state == CREATED || m_sequence_state == STOPPED || m_sequence_state == FINISHED)
{% endhighlight %}
    
邏輯上已經完全不一樣了，所以當 state 不滿足這個條件時立即就會跳出，但是1.0p 不會。我遇到的狀況是連續兩個 phase 呼叫同一個 sequence，而 sequence 的內容是 `forever begin end` ，原本以為 phase 結束會把 sequence 關掉，結果沒有。暫時的解法是先呼叫 `stop_sequences()` 去結束掉原本的 sequence ，再重新呼叫一次。  
The condition is different. It jumps out the task if state does not satisfy the condition but 1.0p don't. The situation I have is calling the same sequence in 2 consequent phases which content is `forever begin end`. It does not stop the first 1 then calls the next as I imagine. Temporarily I call `stop_sequences()` to end up the previous sequence the recall again in next phase to solve it.

2. the physical address of register

![diff of uvm_reg_map.svh](https://lh5.googleusercontent.com/-re7CAWIp7ug/UseSNw0cP-I/AAAAAAAAMKA/E1v6Y9cb0lU/w797-h327-no/Screenshot+from+2014-01-0.png)

可以看到 1.1 比 1.0p 多了幾行，拿 register 的 address 加上 `m_base_addr` ，而 `m_base_addr` 來自於 `configure()`，也就是整組 register block 的 base address；在`add_reg()`時會給定register 一個 *offset*，後來會隱含在 local\_addr 內，這個 offset 在 1.1 有註解說明，是相對於 reg map base address 的位置，但是 1.0p 卻沒有說明。  
There are some lines in 1.1 more than 1.0p. It adds `m_base_addr` which is from `configure()` and is the base address of whole register block to addresses of registers; Besides in `add_reg()` it set a *offset* in register which is implicitly in local\_addr and the relative address to reg\_map base address discribed by the comment in 1.1, but there is no description in 1.0p.

{% highlight verilog %}
// Add a register
//
// Add the specified register instance ~rg~ to this address map.
//
// The register is located at the specified address ~offset~ from
// this maps configured base address.
{% endhighlight %}
    

$$ \textrm{absolute physical address} = \textrm{address}+\textrm{m_base_addr} $$

這樣一來意義就改變了，在 1.0p 時，原本我的寫法是給定絕對位址的，但是在 1.1 時就要改寫成相對位址。  
The meaning is changed. I give absolute addresses in 1.0p, however, they should be relative addresses in 1.1.
