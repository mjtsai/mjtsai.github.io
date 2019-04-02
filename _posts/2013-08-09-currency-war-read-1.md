---
layout: post
title: '讀 貨幣戰爭 - (1)'
date: 2013-08-09 05:47
comments: true
categories: [Finance]
---

![currency war 1-4](http://user-image.logdown.io/user/838/blog/831/post/84441/vZKVfth7RwmsDeHBHiLt_Photo%203.jpg)

自從 2008 金融海嘯過後，同學就推薦我這本書，說是可以了解金融海嘯的一些緣由，基於好奇買來看，愈看愈有興趣，雖然事後再反饋給同學時同學說內容講得太誇張、像是有陰謀論的感覺，但是對於後來發生的 QE - Quantitative Easing (量化寬鬆)、黃金上漲、房市上漲，都能稍微理解其道理，對於一些基本的金融名詞也有些了解，但畢竟自己不是唸經濟相關的，只學過一點會計，如果能用理工的角度來解釋這些現象，應該可以讓自己比較了解。

<!--more-->

首先把每個經濟體都當成一個系統，每個系統的內部財務活動都可以用會計等式的方式來呈現，也就是類似 gnucash 網站裡的圖片這樣 ![accounting equation](http://www.gnucash.org/images/features/basics_AccountRelationships.png)，不過沒像會計那麼正規，同時引入 initial condition 和 boundary condition，這個在微分方程應該很常見吧，不過我都忘光了就是，initial condition 也就是類似一個新的年度時的 balance，有很多時候解釋某些問題直接從一個已知條件開始會比較簡單；另外是 boundary condition，著重在解釋與另外一個系統作財務交換時的行為，系統內部假設使用單一貨幣。


 **以下都是用自己的話講，做個筆記，不一定正確**

很多網站，都已經解釋了銀行形成的歷史，當然是以西方的角度。用我自己的話講，最初的銀行，讓人存放財貨，客戶拿到收據，可以兌換在銀行存放的財貨，藉由收據的信用，收據也就可以當作財貨流通的媒介，也就是**錢**的概念，可以是紙鈔或貴金屬，假設財貨可以用某種度量單位衡量其價值，也就是**元**的概念，因為這樣才能夠將財貨的價值分成小份的交換，但是總數應該和財貨本身的價值相當，也就是，理論上市面上流通的錢的價值應該和存放於銀行財貨的價值相當，兌換率由市場決定。

$$ \sum{ goods \times exchange\;rate(\mathcal{R}) }= \sum{ money} $$


做個推導想像。每家銀行的收據都不一樣，這樣要怎麼保證信用，流通性也受影響，所以，國家可能成立一家銀行，現在叫作中央銀行，把發行收據的權利收回去，也就是**鑄幣權**，私人銀行將財貨與中央銀行兌換錢，兌換率由央行決定，所以財貨大部分集中到中央銀行，私人銀行和人民手上大部分只剩下錢。目前流通的錢的總價值還是等於當初財貨的價值，放在中央銀行的財貨應該就是**準備（reserve）**的概念。如果準備是硬通貨，且如果都是在系統內流動，那貨幣流通量應該會比較穩定。  


$$  
\left(
\begin{array}{l}  
receipt(bankA) \leftrightarrow goods(bankA)\\
receipt(bankB) \leftrightarrow goods(bankB)\\
...
\end{array}
\Rightarrow
\begin{array}{l}
people \leftrightarrow receipt(bankA) \leftrightarrow people\\
people \leftrightarrow receipt(bankB) \leftrightarrow people\\
...
\end{array}
\right)
$$

$$  
money(central bank) \leftrightarrow
\begin{array}{l}
goods(bankA)\\
goods(bankB)\\
...
\end{array}
\Rightarrow 
people \leftrightarrow money \leftrightarrow people
$$



回到古代私人銀行。銀行可不是義務幫人看管財貨的，他們當然也要賺錢的，可以藉由收取保管費、借出等方式賺錢，這些其他資料也講很多了。在不被發現的狀況之下，借出財貨或增發收據這點頗為令人玩味，都代表市面上的收據無法兌換相等的財貨，又代表市面上認為這個經濟體產生的財貨更多，因而可以支持更大的經濟活動，初期反而能刺激經濟發展，但是一旦被發現，表示銀行發行的收據已經失去信用，沒有人要用了吧，大家會想辦法把財貨換回，多出來的廢紙就很麻煩，如果還可以追討，可能會用銀行的財產或者用別人家的收據償還。所以市場會從一個穩態進入暫態再過度到穩態。

回到中央銀行，可能因為某些狀況改變貨幣發行量或改變準備數量，先假設不和其他系統交流，健康的系統，貨幣改變應該是準備改變的效應，因為準備改幣造成貨幣改變，假設交換律不變。
- healthy system

$$
 \textbf{assume } exchange\; rate(\mathcal{R}) \in \mathbb{C}
$$

$$
reserve\cdot \mathcal{R} = money
\Rightarrow
N\cdot reserve \cdot \mathcal{R} = N\cdot money
$$

以增發貨幣來說，印鈔票應該比較容易，逐漸經濟體無法支持增發出的鈔票，供給和需求會失去平衡，例如一天只能做出10個麵包，原本賣10塊，達成平衡，錢變多之後，有些人願意用20塊去買，或是，定價定20塊，去抑制需求，所以物價開始膨脹，另一方面，錢的價值降低，但是就物資與準備的關係而言，反而是回到平衡狀態，例如增發為2倍的錢，一開始還是可以用10塊買到麵包，但其實錢背後的準備含量已經變一半，也就是實際上只要付出一半就可以取得，反而漲到20塊，才是用原本相同的準備去兌換同樣的麵包。增發愈多或準備減少，表示錢隱含準備的量就愈少，所以趨勢不變，持有人會選擇比較保值的方式，也就是換回財貨，在還沒崩盤之前，可以叫做避免通貨膨脹而投資，在通貨膨脹的系統裡，持有財貨會比持有鈔票好，所以為什麼說富者愈富、貧者愈貧，因為富人會把可支配所得換成資產保存，而不是錢，窮人比較常持有錢而已。如果崩盤，那就是信用破產，沒人要用這個系統的貨幣了，暫態應該會使用其他替代品去交換財貨，和私人銀行信用破產類似，直到有新的令人有信心的貨幣出現為止，拿舊的貨幣兌換新的貨幣，兌換的程序又回到銀行和央行兌換的程序。
- unhealthy system

$$
\begin{array}{l}
    reserve \cdot \mathcal{R} = money\\
    \Downarrow\\
    reserve \cdot \mathcal{R} \neq N\cdot money, N\gg 1\\
    \Downarrow \textbf{for a while}\\
    \textbf{implicitly believe } N\cdot reserve \cdot \mathcal{R} = N\cdot money \\
    \Downarrow \textbf{finally}\\
    \frac{reserve}{money} = \frac{1}{\mathcal{R}} \rightarrow \frac{reserve}{N\cdot money} = \frac{1}{N\mathcal{R}}\\
    \Downarrow \textbf{collapse}\\
    \begin{array}{lllll}
        money &\rightarrow &goods &\rightarrow & new\; money\\
        (N-1)\cdot money \cdot 1/M&\rightarrow & new\; money
    \end{array}\\
    \Downarrow \textbf{restablize}\\
    new\; reserve \cdot \mathcal{R'} =  new\; money
\end{array}
$$

