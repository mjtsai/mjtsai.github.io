---
layout: post
title: '用 GnuCash 記帳 Accounting with GnuCash - 4'
date: 2015-02-19 11:13
comments: true
categories: 
---
很久沒更新了，之前寫的在這邊，因為有些紀錄方式後來覺得不太對，需要改正一下  
[用 GnuCash 記帳 Accounting with GnuCash - 1](http://mongala-memo.blogspot.tw/2011/03/gnucash-accounting-with-gnucash-1.html)  
[用 GnuCash 記帳 Accounting with GnuCash - 2](http://mongala-memo.blogspot.tw/2011/03/gnucash-accounting-with-gnucash-2.html)  
[用 GnuCash 記帳 Accounting with GnuCash - 3](http://mongala-memo.blogspot.tw/2011/03/gnucash-accounting-with-gnucash-3.html)  
<!--more-->

1. 對於股票，原本想說每年計算每年的損益，因此在當年度還留有股票資產時，結算就用(封關價-當年平均成本)當作損益，但這樣真的滿麻煩的，其實我只在乎資產增加多少而已，每年的變動並不在意。所以修改成只有有交易才紀錄損益，沒有交易的部份，就繼續當成資產延到隔年。配息的部份，當成收入，而配股的部份，當成資產增加，配合收入增加，不考慮因為配股配息造成淨值變低的結果，未來賣出時，以最先買進的價格當作損益基準。

2. 外幣同上

3. 今年遇到一個新問題，在年度當中，當我要把某個項目完全轉到另外一本去接著紀錄要怎麼作。在網路上找到一個方法是，將這個項目歸0，平衡項記在 open balance，在新的帳本中開啟這個項目，同時也記在 open balance，表示從這個時間點開始紀錄。

4. file -> export -> export account 可以把項目全部複製到新的檔案，不用自己重新打一次




#### 待解決的問題

1. 同時有多本帳本，匯款到另外的帳戶時，不知道這些增減應該怎麼記，如果記收入支出的話，覺得不太合理，因為轉出不等於支出。

2. 不知道有沒有工具可以處理跨多本帳本，算出年度總結果的。

3. 不知道有沒有工具可以在開啟新帳本時，把最後的資料複製過去，這樣就不用重頭再輸入一次



