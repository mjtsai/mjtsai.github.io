---
layout: post
title: 'IC驗證工程師?'
date: 2015-05-23 11:35
comments: true
categories: [verification]
---
> RTL implementation 是無到有，dv 和 ESL 是有到好


前陣子 ptt 上開了這篇討論文，忍不住又想靠北一下，做了超過 5 年的 dv，作過超過半顆 SoC 的驗證，是還有很多沒碰到  
[https://www.ptt.cc/bbs/Tech_Job/M.1431170689.A.51B.html](https://www.ptt.cc/bbs/Tech_Job/M.1431170689.A.51B.html)  
[https://www.ptt.cc/bbs/Tech_Job/M.1431228765.A.99E.html](https://www.ptt.cc/bbs/Tech_Job/M.1431228765.A.99E.html)  
[https://www.ptt.cc/bbs/Tech_Job/M.1431232046.A.E16.html](https://www.ptt.cc/bbs/Tech_Job/M.1431232046.A.E16.html)  


以下單純抱怨，我的職涯所見所聞還是很狹隘，也許在偉大的航道上有人會覺得我怎麼作的那麼差
<!--more-->

2015 年開始，傳說，dv 的工作機會變很多，需求很大，哇哩  ... 是趕流行吧。這裡的 dv 指前端驗證，不管是 fpga, emulator, uvm, formal, in-house methodology，**但此篇會排除 fpga**，在台灣要當純職 dv，請找大 designe house 或是外商、vendor、不然就出國，因為很重要所以說三次。(雖然我不知道國外是否真如討論說的資深的來作 dv 、dv 被重視，不過有聽說過外國用 high-level synthesis 作IP，所以給 RTL 沒關係，dv和 fw 留國內)

但是找大 design house 就一定好嗎？聽說麥當勞的某位處長說過以前沒有 dv team 也一樣可以 tape out 啊 (這裡必須要把 fpga 排除，因為歷史的緣故，前輩們的 fpga 功力都超高，拉拉 LA 就可以 debug)，聽麥當勞的同事講 dv 也是 designer 說一動作一動(看部門)，也找大陸人；聽說滷肉飯以前就用 fpga 跑系統驗證，何必要 dv，104 開出來也是 design缺含  dv加分，全職dv就像開發 flow 而已；子公司的x總說 dv 不就是 random 而已；作小 IP 的公司更不用說了，也是說就用 fpga 驗啊，比 simulation 跑的時間久，pattern 又多，何必 dv，所以說 dv 根本不重要。

dv 在公司的地位一定比 designer(泛指 RTL implementation) 低，在常態分佈上被認為，designer 懂 dv 而 dv 不懂 design，dv 可以換成 sd, apr 等等，比較 junior 的 designer 要從驗證做起。難道妙麗一直都是第一名就會被認可為巫師嗎？當你認為 design 上有錯誤或是對 sw 來說不好用時，人家還覺得你找麻煩哩;當你覺得還沒驗完時，人家還覺得你 delay schedule 哩；有 bug 時就會被怪沒驗到；分紅時老闆只記得 hw，sw 很辛苦，dv 分的錢也比較少，就算你貢獻很多。

教科書上面都說驗證的時間佔整個 project 時間 70%+ ，而且驗證難度成指數次方成長。事實是，時間到了就要 TO，誰管你。有問題再 ECO ，有錢就是任性嘛。

designer 也有很多其他事要作，自然有 designer 去靠北。designer 可以發專利，就算是一個很快就被淘汰的東西，可沒聽過 dv 發什麼專利(不過可以發 paper)；designer 可以創業，沒聽過 dv 創業的，作 tool 算嗎？大概作到被三巨頭買下來就算成功了吧，不過想做軟體，web 和嵌入式這麼夯，幹嘛作 tool。

dv 的重要性，相依於產品的複雜度、工藝和價錢，能不能佔據一個重要的地位，就看你能夠處理多複雜的問題。designer -> architect、integrator，dv 永遠低一截，難道只能這樣嗎？ 在前端階段，我就不覺的 designer, architect 會比較厲害。＄0.1的產品可以不重視 dv、>40nm 的可以不重視 dv、低速 IC 可以不重視 dv(連apr 都可以不重視)、只做 IP 的可以不重視 dv，但是 $10 的 IC 可以不重視 dv 嗎？ \<28nm 的可以不重視 dv 嗎？ >1Ghz clock DVFS 可以不重視 dv 嗎？ 作 HSA + codec + modem + OS 的 SoC 不用重視 dv 嗎？(flip-chip、hot-spot、power-domain、CTS 能不注重 apr嗎) 

> 功夫沒有好壞之分，只有功力深淺

有多專業，地位才有多高～(不過還是有被說過會的東西太雜沒有專業)，dv 也是有等級之分的
- 你可以指出 spec 上的問題，提供軟硬整合的意見，修改 RTL，還是只是聽 designer 講的去作。

	不要覺得 designer 比較高貴，雖然業界就是如此，designer 常常很多都不太清楚，很多時候也只是當接線生，IP 接上去完事，根本不懂怎麼操作；很多時候做出來的東西 sw 根本就很難用、增加錯誤、降低 performance，而且驗證時間也是成指數方成長，不過他們也只求一個可以動就好了，最好挑簡單的測一測交差了事，有 bug 最好可以 sw workaround，反正 performance 低賣便宜一點就好了。
- 你可以整合不同 IP ，還是一個 IP 就處理不完了。
	IP 也要分等級，處理 CPU，我相信一個 IP 就很複雜，難度相當於很多小 IP，但是如果只會一個 uart，這樣是不夠的。
	很多時候，module level 的測試根本不夠，VIP 很可能沒有描述真實 IP 的行為，導致有些沒測到，這點在 in-house IP 比較可能出現，買來的標準 protocol 通常很完整。(但是相對而言，sys level 可能打很久都打不出某些特定狀況)
  不得不說如果 designer 有接線生，那 dv 也有，VIP 接上去就完事，vendor 給的 suite 移植一下，跟本不知道在測什麼，要改也不知道怎麼改。
  說到這裡就覺得三巨頭賺很大，design house 根本就在作整合而已，很多東西都買 IP 就好啦，可能還比自己作便宜。
  討論說到 top-level，其實 dv 的價值會在這邊浮現，因為很多作 design 根本守著一個 IP 好多年，不一定會知道整起來到底應該會怎樣，但是這算是 dv 的基本吧，都已經被說沒專業了當然要多懂一些。
  
- 你可以整合軟體、數位、類比，還是光是數位就處理不了了。

	目前我也只會向下整到 PHY 的 digital 部份，mixed-signal 還不知道怎麼整；軟體的部份也還沒進到 OS ，看人家前段可以跑 android 真感到汗顏。有些驗證是彼此重疊的，這樣降低個人的重要性但是可以提昇穩定度，像是 mixed-signal 會在板子上再驗一次、下 test chip，OS 以上的軟體部份會用 fpga 或是 emulator 驗。
  
- 你可以整合不同 methodology ，uvm+emulator , uvm+software , uvm + c model ，還是只會一種。

	都會可是還不夠，繼續朝 systemc co-sim 的道路邁進。
  
- 你可以分辨哪種平台適合哪種應用嗎？還是就埋頭硬幹。

	討論說 emulator 的人很少，因為沒幾家公司買得起好嗎！一台要好幾百萬鎂，還有每個月要付電費耶，如果沒有需求就用 fpga 就好啦，再次覺得三巨頭賺很大，要很感恩的確是公司付錢讓你學習，有問題就把 AE 找來拉正就好啦。emulator 就是很貴的高級 fpga，不過彈性增加很多，可以混搭 simulator，visibility 可以增加，但是速度就會在資料交換時降低很多，所以，就算有 emulator，如果不能善用的話，可能效益還不如 RTL2C 或 fpga。
  和 fpga 一樣，emulator 也需要 synthesizable RTL，不過也可以合成一些 non-synthesizable 的語法啦，最好能夠全部合進去，但是這樣原本在 simulation 能夠使用的環境很多又要重刻，才能夠享受其優點，但如果因此精簡掉很多細節的話，就不能確認驗證是否有效。
  systemverilog 能夠處理較為 critical 的狀況，controllability、visibility 也最高，缺點就是一般 simulator 的缺點，速度慢啊！systemverilog 適合懂軟體的人來寫，才比較能享受 OO 的好處，當你看到用 systemverilog 還在寫 state machine 和 bit-level 的處理時，會覺得很不優雅。
  PO 軟體上平台就是要驗真實軟體的狀況，只會用到 subset ，而不一定會用到所有 function，也不一定會測到所有的行為，就算跑的時間更長，如果因為軟體不用就不驗，那不太適合作這行，心態就有問題。
  fpga 有很大的需求，但很多人都不想碰，要自己搭環境，過程中還可能遇到很多合不出來的問題，就這樣。fpga 沒辦法驗全速，頂多跑在相同 clock 比例，簡單來說就是降頻跑，但這樣會漏掉只有在全速才會出現問題。目前三巨頭有出貴鬆鬆的fpga 整合平台，前端軟體又變得比較好用，有錢的話可以買來用用。
  
- 你是發展 methodology的人，還是執行的人。
	
	還沒有能力作比較精確的說明。但可以這樣說，發展 methodology 類似發展 uvm，要能夠達成某種目的、架構清楚、可以擴充、可以重用，最好是有軟工基礎和 domain knowledge，像是規劃 design pattern 那樣；執行的人，就像是拿 uvm 來寫 VIP，將其特例化。
  如果只按照 vendor 的 flow 而無法加以變化的話，亦非上乘。
  能夠開發 in-house methodology 的話，才能夠學到最多東西，混合不同語言和平台來作分析最有趣了，而且是 designer不懂的。但是相對的，被 in-house methodology 綁住的話，去外面又找不到工作，好難取捨啊～～

- 你可以驗 function , performance , power ，還是 function 就驗不完了。

	function 玩到很無聊，無奈舞台不夠大，想做 system 等級的 performance 和 power 分析，會去注重這兩項的產品也不多吧。
  
驗證的領域很廣，但是在業界是非必要條件、不受重視，成長空間也不大，所以如果沒興趣，還是找比較夯的工作比較好。

#### 20161029 ptt 轉貼
[[心得] IC驗證工程師工作經驗分享](https://www.ptt.cc/bbs/Tech_Job/M.1477695484.A.74C.html)  
[Re: [心得] IC驗證工程師工作經驗分享](https://www.ptt.cc/bbs/Tech_Job/M.1477790501.A.6BB.html)  
[Re: [心得] IC驗證工程師工作經驗分享](https://www.ptt.cc/bbs/Tech_Job/M.1477822757.A.CD5.html)  
作者是在MTK
  
