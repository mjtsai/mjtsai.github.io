---
layout: post
title: 'UVM note - (5) response queue overflow in RAL test'
date: 2013-12-24 16:31
comments: true
categories: [uvm, verification]
---
在串 RAL built-in test 時遇到的問題，就是 response queue overflow ，因為 default response queue depth = 8 ，也的確看到 8 個正常的 transaction 後發生 overflow ，原因是因為我的 sequencer 用 ``item_done(rsp)`` 去回應 RAL ，這會把 rsp 推進 response queue，但卻沒有人把他拿走，所以才 overflow。
I had some problem during making RAL built-in test, the response queue overflow due to default response queue depth = 8 and exactly it is overflow after 8 transactions passed. It is because I used ``item_done(rsp)`` in the sequencer to response RAL which pushes rsp into the response queue without got by anyone.

解法 : 
1. 設定 `adapter.provides_responses=1` 可以解決這個問題，在 call adapter 時會去 call `get_response()`。
2. 或是 sequencer 用 ``item_done()`` 去回應 RAL。

solution : 
1. set `adapter.provides_responses=1`. It calls `get_response()` while calling the adapter。
2. use ``item_done()`` in the sequencer to response RAL。

不過令人感到疑惑的是，只有在測 built-in test 才出狀況，其他使用 RAL 的情況並沒有出現。
However I am confused to the problem is only in makeing built-in test but other situation applied RAL.

REF : [get_response() with UVM RAL](https://verificationacademy.com/forums/uvm/getresponse-uvm-ral)