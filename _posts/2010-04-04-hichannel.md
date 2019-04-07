---
layout: post
title: hichannel廣播位址解析
date: '2010-04-04T23:26:00.000+08:00'
author: mjtsai
tags: misc
modified_time: '2010-04-04T23:34:44.927+08:00'
blogger_id: tag:blogger.com,1999:blog-6729751024593483406.post-3302426007249074077
blogger_orig_url: https://mongala-memo.blogspot.com/2010/04/hichannel.html
---


-- 2009/11/14 bbs backup --
<!--more-->

不好意思玩太晚了  

因為最近上班都在聽廣播，我要推薦奇美古典音樂網，但想用foobar來放時竟然沒辦法解析，而且hichannel 用微軟的東西，導致我的電腦也不能放，先抓了 fourDollar(其實我見過他本人耶)的hiChannel.sh來執行，他會直接取得 [http://hichannel.hinet.net/player/radio/index.jsp?radio_id=#](http://hichannel.hinet.net/player/radio/index.jsp?radio_id=#) 從裡面取得真正的位址 [mms://bcr.media.hinet.net/#](mms://bcr.media.hinet.net/#) 但我很好奇有些文章說hichannel的格式改變了，為了瞭解位址是怎麼來的，就手動trace了一遍，反正最近也在trace code


1. 先從連結進入 [http://hichannel.hinet.net/radio.do?id=#](http://hichannel.hinet.net/radio.do?id=#)

2. 在播放面板的註解位置會看到 `src="player/tPlayer_radio.jsp?id=#"`
                                                                               
3. 取得此檔案後，開始照著教學，找到 `window.open` 下的 `radio-f1.jsp?id=#`，手動取得檔案

4. 此檔案下的`MediaArea` tag 內有`src="_radio-f1.jsp?id=#"`，手動取得檔案

5. 此檔案下搜尋 mms 就可以找到原始位址 `mms://bcr.media.hinet.net/#` 了

不過後來發現在步驟2搜尋 mms 就有原始位址，不用再繞一大圈
