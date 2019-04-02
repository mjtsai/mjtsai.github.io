---
layout: post
title: 'UVM note - (8) multi-layered sequencer'
date: 2015-05-23 01:43
comments: true
categories: [uvm, verification]
---
我不喜歡 `default_seqeunce`，這樣很沒彈性，不過教科書都會這樣教，因為教科書就是教入門的嘛，但是我的應用需要多次更換 sequence，例如 PHY plug detection -> PHY functional，我不想用什麼 state machine 去寫，那樣太不優雅了。
<!--more-->

前陣子同事分享了 mentor graphics 的 multi-layered sequencer 教學，結果我發現在幾個月前已經不一樣的方式實現完成了，而且這篇教學有個問題，他使用 handle 去指向另一個 sequencer，好處是不用透過 port 相接，可以精簡一些執行的 loading ，但是如果想改變 handle 的 type，就無法達到重用的目的。

我是用 port/export 相連接的，這樣作比較麻煩，但我的確重複利用了以前的 sequencer/sequence。其實出發點應該反過來，我是因為想要重複利用以前的 sequencer/sequence ，才做出 multi-layered 這種架構出來，這樣我只要加個 transactor 來連接舊的和新的 sequencer 就好（如果用 OO 的方式應該用 adapter pattern）；另一方面，我實作的 protocol 本身就是適合多層級的架構，就像是 OSI model。 Multi-layerd agent 我已經作過了，至於要用 multi-layerd sequencer 還是 agent，看整個系統如何區分會比較好。至於所謂一個 agent 搭配一個 sequencer 的原則 ... 我完全不管教科書要怎麼講，而且如果是輕量的 sequencer，再多包一層 agent 是多此一舉。

我記得我是參考 Dulos 的網站找尋靈感的，但我忘了是哪篇，我的作法只用 sequencer 處理，不包含 monitor。

其實 sequence 才是靈魂，flow 非常簡單，怎麼想就怎麼作，而且困難的也不是 transmitter ，而是 receiver。

* tx
{% highlight verilog %}
upper_port.get_next_item(upper_item);
... do something ...
`uvm_send(to_lower_item)
upper_port.item_done();
{% endhighlight %}

* rx
{% highlight verilog %}
upper_port.get_next_item(upper_item);
`uvm_create(to_lower_item)
`uvm_send(to_lower_item)
get_response(to_lower_item)
... do something ; copy info from to_lower_item to to_upper_item(can be = upper_item) ...
upper_port.item_done(to_upper_item);  / upper_port.put_response(to_upper_item);
{% endhighlight %}

比較有趣的是，如果 to\_upper\_item 和 to\_lower\_item type 相同的話，是不是就不需要作 copy data，我知道 copy data 非常耗資源，但是 sequence id 不同，所以直接把 to\_lower\_item 往上丟，會收不到，這邊有個不錯的解法，[seq\_item\_port.put\_response(rsp);](http://forums.accellera.org/topic/338-seq-item-portput-responsersp/)，只要 copy 必要的 info 就好了；如果 type 不同，那就是整個資料結構都要 copy，無法精簡。

