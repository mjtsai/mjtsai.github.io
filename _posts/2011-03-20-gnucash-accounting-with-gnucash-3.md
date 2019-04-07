---
layout: post
title: 用 GnuCash 記帳 Accounting with GnuCash - 3
date: '2011-03-20T10:43:00.000+08:00'
author: mjtsai
tags: finance
modified_time: '2011-07-02T12:14:21.771+08:00'
blogger_id: tag:blogger.com,1999:blog-6729751024593483406.post-9121186505995088421
blogger_orig_url: https://mongala-memo.blogspot.com/2011/03/gnucash-accounting-with-gnucash-3.html
---

外幣的觀念也是一樣，因為是以新台幣為出發點，最後就要換回新台幣結算，因此和股票一樣，新增一個外幣計價的項目，將台幣轉換過去，也是一樣是資產轉換，結算也是一樣換成封關來結算，只是，記錄盈虧比較怪異一點。

[Tracking Currency Investments (How-To)](http://svn.gnucash.org/docs/guide/currency_invest1.html)

和股票一樣，盈虧需要一個平衡項，這個平衡項也是外幣，但是如果直接登記在外幣項的話會讓外幣增加，這是不對的，參考manual的作法，先登記獲利或虧損，再登記外幣的平衡項，這時後會跳出匯率視窗，要登記轉換總數為0，也就是匯率為0的意思，這也是一個虛項，將台幣計價的獲利或虧損轉換成價值為0的外幣。

$$
\begin{array} {rclcl}
cash\_old &\rightarrow & other\ currency & = \\
cash\_new &\leftarrow & other\ currency & = \\
&& other\ currency(0) &=& gain\ or\ loss\\
(ignore\ fee)&&&\\
cash\_new - cash\_old &&& = &gain\ or\ loss 
\end{array}
$$



配股配息一樣要入帳，配股比較簡單，但是我還沒遇過，也許有錯，配股其實只要把股票項增加就好，因為股票項是隱藏的，也不會影響平衡；反之配息會讓現金增加，不得不考慮平衡的問題，首先配息會讓股價成本降低，要做個假的賣出和買進(如果有處理配息的功能的話，就不要照我這樣做)，這樣會讓現金增加，同樣的錢不可能憑空增加，要再加一筆收入去平衡。

$$
\begin{array} {rcl}
stock\_old\ sell - stock\_new\ buy + cash &= &\\
stock(hidden) &=& dividend\ income
\end{array}
$$


BTW，這一年也遇到公司合併，就會有股票轉換的問題，這就簡單多了，只要把原股轉新股就可以了。

整本帳簿的結算其實很簡單，只要選 Tools/Close Book，就會自動把 Income 加總，Expense 加總，然後相減，列入Equity 這項，基於 $$Assets = Liability + Owner's Equity + (Income - Expenses)$$ 的原則，就可以檢查得出來自己的總帳目有沒有平衡，只要有如實記錄，理論上應該是平衡的，要是我念英文有像記帳那麼有恆心就好...。

