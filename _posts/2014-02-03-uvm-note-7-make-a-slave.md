---
layout: post
title: 'UVM note - (7) make a slave'
date: 2014-02-03 10:48
comments: true
categories: [uvm, verification]
---
> to be a master rather than a slave

### Definition here
   master 會主動發起 transaction ，但是 slave 不會，slave 是收到 transaction 後才會回應 transaction 或是一直接收 transaction。或是可以叫做 responder。是一個**被動的** module。  
   Master initializes a transaction but slave don't. Slave responses a transaction after receiving or continuously receives. Also known as a responder. It's a **passive** module.

<!--more-->

### The practical problem

我上過的課或是我看過的例子都是 master component。Flow 都按照下面的模板  
Courses I've taken and examples I've studied always give the master components. The templates follow the flow, 

```verilog
get_next_item();
...
item_done();
```

這就是 - transaction 是由 sequence 發動的接著 driver 再將 transaction 輸出到 wire 上，包括了傳送信號或是從對方取得資訊。但是，在許多應用是需要 slave component 的。不僅僅只是在 signal level 可以處理的簡單狀況，例如 decode bus protocol 再把 data 存入 memory model。考慮以下狀況：

1. 對 slave 來說，第一個 transaction 不是從 sequence 來而是從 driver，他需要在 request 之後做回應。(也可以用上面的 flow 做，但有可能整個 test 都等不到第一個 transaction，sequence 無法完成) 
2. 有些比較複雜的 protocol 在 transaction level 會比 signal level 好處理，像是許多 serial I/O protocol。
3. 一個完整的複雜 I/O protocol 需要傳送及接收 command/data，我想把一個 command 作在一個 sequence 內。


That is - the transaction is initialized by the sequences and then drivers send out the transaction on the wires, including send signals to or get some info from the other side. However, in many applications, it needs the slave component. Not only the simple scenario that you can deal all things in signal level, e.g. decode the bus protocol and put the data to a memory model. Considering these scenario,  

									                              
1. For a slave, 1st transactions are not initialized by sequences, it is by drivers. It should respond after receiving requests. (The above flow can also be applied. But there may be no 1st necesssary transaction arrivesto make the sequence uncomplete.)
2. Some more complex protocols are easy to handle in transaction level than signal level, such as many serial I/O protocols. 
3. A command of complex I/O protocols has to transmit and receive command/data. I want to develop a command in a sequence.

我需要的是一個較容易擴充而且容易開發的架構，我想要把大部分的實作都放在 sequence stack 內，因此我可以

1. 將所有的 protocol command 都放在 sequence 內，而不是在 signal level 放一個很大的 state machine 或 ``case()``。
2. 在同一個 sequence 內實作一個 command 的傳送和接收。
3. 將連續接收的 transaction 分給不同的 sequence

What I need is more scalable and easy to code architecture. I want to implement most part in sequence stack. Thus I can

1. create whole commands of the protocols in sequences rather than a big state machine or ``case()`` in signal level.
2. implement both of transmission and receipt of a command in a sequence.
3. assign continuous received transactions to different sequences.


### Implementation

接著是兩個部份：
1. 動態掛起需要的 sequence 
2. 把 transaction 放到正確的 sequence
這是我所想的以及實作的解法，不是 template 或是研究。

Following are 2 parts: 
1. dynamically hookup sequences whenever needed 
2. put transactions to the correct sequences. 
They are what I think and my solution, implementation, not the template or some kind of research. 

#### Dynamically hookup sequences whenever needed

![hookup_seq](https://lh3.googleusercontent.com/-aDldjdNYVo8/UvD1OpcTziI/AAAAAAAAML4/tQC-uUj4LMU/w1276-h598-no/hookup_seq.png)

我決定按照傳統的 flow 在 *agent* 內建立新的 sequence 然後在 sequencer 啟動，decode 信號後可以知道 response 的需要，receiver 就會呼叫 agent 內的 `write` 透過 analysis port 把解碼後的 transaction 送到 agent，接著 agent 就會建立需要的 sequence 然後把從 driver 得到的 transaction 推進去。

I decide to create new sequence in *agent* then start it in the sequencer which is following the conventional flow. Knowing the need of response by decoding the signals, driver calls `write` in agent to send the decoded transaction to agent through analysis port. Then agent creates the necessary sequences and put the transactions from driver to it. 


#### Put transactions to the correct sequences

`item_done()` 可以用來把 transaction 送回 sequence，但是直接把收到的 transaction 送進 sequence 是沒有作用的，在之前的文章 : [uvm_response](https://logdown.com/account/posts/98732-uvm-note-3-response/edit)，提到需要 *sequence id* 來辨認 transaction 是從哪個 sequence 過來，但是對於收到的 transaction 來說，**他不是從任何 sequence 過來的**，在這段code，他會判斷為錯誤。

The `item_done()` can be used to transfer transactions back into the sequences. But it does not work if you put the received transaction to a sequence directly. In my previous artical: [uvm_response](https://logdown.com/account/posts/98732-uvm-note-3-response/edit), it mentioned that a *sequence id* is needed to identify which sequence is the transaction from. However for a received transaction, **it is not from any sequence**. In this piece of code, it may judge it as an error. 

![put_response](https://lh4.googleusercontent.com/-zp5npZUeO0Q/UvD8mVuCjzI/AAAAAAAAMMM/ZYsDYbFiOdM/w1272-h348-no/Screenshot.png)

因此，我必須在他被建立時取得 sequence id 然後再將 id 賦與 transaction，所以被收到的 transaction 可以安全地被送到 sequence 以及被 `get_response()` 使用。

Therefore, I have to get the sequence id after it is created then assign the id to the transaction. Thus the received transaction can be safely sent to the sequence and can be used with `get_response()`.

### After This
這是建立在 master 和 slave 都是 **standalone** 的情況下，所以 slave 要從第一個 transaction 後才回應，但是如果 test 直接控制這兩個的話，問題就變簡單了。你可以在 *virtual sequence* 內控制這兩個元件，使得 slave 可以預測到 master 會送什麼 transaction，並像教科書一樣準備好相對應的 sequence。

The assumption is the master and slave are **slandalone**. Thus the slave must respond after receiving 1st transaction. However, if both the two can be controlled by the test, the problem is simpler. You can control the two components in the *virtual sequence* to make the slave predict what transactions from the master and prepare the corresponded sequences in the reference flow of text book.
