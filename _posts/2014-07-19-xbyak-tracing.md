---
layout: post
title: 'xbyak tracing'
date: 2014-07-19 08:43
comments: true
categories: 
---
[xbyak](https://github.com/herumi/xbyak) 是一個 open source 的 JIT(just-in-time) assembler，他可以在 runtime 時建構 x86 instruction，然後執行，常被拿來做 cpu simulator。開發者的話，建議要懂得 x86 的組語怎麼寫，function 怎麼傳，像我是不太會的。
<!--more-->

最近花了幾天 trace 一下 xbyak 的主流程，有點收穫。可以先從 sample 開始看並且執行，例如 brainfuck compiler，可以參考 jserv 的文章 [打造 Brainfuck 的 JIT compiler](http://blog.linux.org.tw/~jserv/archives/002119.html)。

JIT assembler 的觀念就是在 runtime 生成 host machine code ，再去執行。因此，xbyak 有 2 個 class 比較重要：1. **Xbyak::CodeGenerator** 用來生成 machine code , 2. **Xbyak::CodeArray** 用來儲存產生出來的 machine code。在範例之中可以看到，main 內會 instance 一個主要的 class，這個 class 繼承 Xbyak::CodeGenerator，在 constructor 時就會建立 x86 machine code，但是實務上並不一定要在 constructor 就實作所有的功能，接著使用 getCode 把 x86 machine code 指標抓出來，再用 **function pointer** 的方式執行，因此，在建構這個 class 的功能時，要想像成是一個具有功能的函式，且必須要滿足 call function 的步驟，例如進 function 要 push、出 function 要 pop。這大概就是使用 xbyak 的基本 flow。

class 建立時必須要繼承 Xbyak::CodeGenerator，且一個 class 代表一個 function，在 CodeGenerator 內已經有實作常用的 mapping function，call 這些 function 就可以轉成相對應的 x86 instruction，撰寫時用 x86 assembly 的角度去寫就可以，最終會把轉完的 machine code 放到 CodeArray 裡。

CodeArray 的 top\_ 指向最終 machine code 放置的 array，在 windows 會用 	``VirtualProtect`` 、linux 用 ``mprotect`` 去把這塊 memory 的權限設成可執行(executable) ，因此之後才可以呼叫他；這塊 memory 也是可以自動調整大小，所以不用擔心會用超過；getCode 會傳回指定型態的 function pointer。




