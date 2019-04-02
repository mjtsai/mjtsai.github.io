---
layout: post
title: 'verilog binary semaphore'
date: 2015-12-06 15:33
comments: true
categories: [verification]
---
REF: [How to write SystemVerilog-like semaphore in Verilog?](https://groups.google.com/forum/#!topic/comp.lang.verilog/fFdfqzzK8B4)

去年需要實作新的 bench ，但又必須在舊的 verilog 上開發，實在不是很方便，要知道 systemverilog 在處理 multi task 方面增強了很多功能，例如原生 semaphore。所以我只好上網找了一個，這個實作比較像是 mutex 的功能，也符合我對於 shared resource 的需求。

這個實作，每個 requester 都會帶個 id ，依照 race condition 的結果紀錄最後贏的 id，此 id 的 requester 會回到主程式繼續向下，其他的 requester 會被 block ，直到這個 requester unlock 為止，再進行下次的 arbitrate。藉由不斷在 delta T 內觸發 event，來讓被 block 住的 task 被喚起進行搶佔。

這個實作需要對 simulator 有更深的了解，像是把 non-block 和 blocking 寫在一起的作法，我是著實花了一些時間搞懂。不過拿來用之後發現當 lock / unlock 之前如果時間有前進的話，這個方法會有問題，因此又做了一些修改。