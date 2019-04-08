---
layout: post
title: Those Things about Memory Mapping ... / Memory Mapping 的那些事
date: '2012-11-11T11:40:00.000+08:00'
author: mjtsai
tags: program
modified_time: '2012-11-11T11:40:05.053+08:00'
blogger_id: tag:blogger.com,1999:blog-6729751024593483406.post-5162476766366666538
blogger_orig_url: https://mongala-memo.blogspot.com/2012/11/those-things-about-memory-mapping.html
---


I have just learned computer architecture but OS so never linked them at all. These days I finished tracing a sample bootcode and read the arm programming guide. A sentence caught my eye which means every process has its own memory mapping, there are many page tables on runtime. I was too stupid to think there was only one page table where one program occupied part of memory and the code followed the rules in the part of memory, instructions on the bottom, stack on the top... Another impact was that it could allocate new memory by updating the page tables. I never knew it.
<!--more-->

Several days after that day, I continuously construct the imagination of the code arrangement in the memory mapping, how the OS deals with the page tables. I only know that one program must ask the OS to get more space.


Discussing with one of my colleagues in SW team and looking for some information, my imagination is very close to the real case but remains some problems to solve, e.g. share libraries. [Understanding Memory](http://www.ualberta.ca/CNS/RESEARCH/LinuxClusters/mem.html#mmap) describes very clearly.



My Descriptions

Codes in a process are mapped to whole virtual memory space, i.e. 4GB in 32b system. OS finds unused spaces and updates the page table to map these codes to appropriate spaces. When it needs to allocate more space, OS searches free spaces in memory then update the page table of the process so that it can access the spaces.


