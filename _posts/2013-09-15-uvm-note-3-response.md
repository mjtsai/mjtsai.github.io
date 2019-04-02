---
layout: post
title: 'UVM note - (3) transaction flow - response'
date: 2013-09-15 04:17
comments: true
categories: [uvm, verification]
---
來討論一下前面那篇沒有提到的 response flow。  
To discuss the response flow which is not mentioned in previous post.

<!--more-->
這張圖簡略說明一個 sequence item 如何走到需要它的 process。透過 trace 程式碼，可以知道它是用 *sequence id* 來知道要傳到什麼地方，當 sequence 或 sequence item 開始執行的時候，他會送一個 request 給 sequencer，在 sequencer 內註冊自己，而 sequencer 會分配一個 *sequence id* 回去。sequence 有自己的 id 而 sequence item 是依附在 sequence 上。  
The diagram concisely describes how a sequence item pass through each component to the process need it. Tracing the code, you may know it recognizes where to send the sequence item by the *sequence id*. At the begnning the sequence executes or the sequence item send request to the sequencer, they make a register in the sequencer and sequencer gives the unique *seqeunce id* back. The sequence has its own id but the sequence item has the id of the sequence want to send it.

當 driver 回應一個特定 sequence id (不等於 -1) 的 sequence item 時，sequencer 會用 sequence id 當成 key 去搜尋他的資料庫，然後把 sequence item 傳給相對應的 sequence，然後 sequence 就可以拿到 sequence item。  
At the time the driver make a response with a sequence item with a specified sequence id (neq -1) to the sequencer. The sequencer searches a sequence in its database by the sequence id as key, then bypass the sequence item to the sequence. Then the sequence can get the sequence item.


![uvm_transaction_response.svg](https://drive.google.com/uc?id=0Bxm9QxsD8PDPa0F5Y3c2Qzd6SjQ)
