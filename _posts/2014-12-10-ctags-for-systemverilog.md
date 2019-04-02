---
layout: post
title: 'ctags for systemverilog'
date: 2014-12-10 00:18
comments: true
categories: [verification]
---
我們知道 vim+ctags 是寫程式時很強大的組合，但是原本的 package 似乎沒有 systemverilog 的支援，不過在網路上有找到有人幫忙寫了 systemverilog 語法的支援。  
vim+ctags are well known tool combination for programming. 
<!--more-->

## add systemverilog filter

http://kaushalmodi.github.io/2014/03/09/ctags-verilog-and-emacs/

但是還缺少 covergroup 、clocking 、constraint 的語法，因此又參考別的網頁將他補上

https://github.com/shaohao/config.d/blob/master/ctags

## import UVM library tags in vim

```ctags -R <path/to/UVM/src>``` 會產生 uvm library 的 tags，但是要怎麼在別的地方使用而不用再 parse 一次呢？

https://coderwall.com/p/fy7stg/vim-and-systemverilog

這裡有提到可以在 ```.vimrc``` 內設定載入 tags 時所包含的路徑，目前我是設定``` set tags=./tags,tags,~/.vim/tags/UVM```，```./tags``` 表示開啟檔案所在目錄的 tags ，```tags``` 表示現在目錄的 tags，原本以為只要其中一個就好，結果開其他路徑發現沒作用，這樣就可以了。




