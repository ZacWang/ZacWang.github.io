---
title: visual studio 2015 bug about git source control
date: 2016-03-16 10:00:11
categories: visual studio
tags:
---

visual studio 2015增加了对git以及github的支持，但是使用过程中有一个问题，在向解决方案中添加了一个c的lib项目后，git无法正常工作。

<!--more-->

参考：[stack overflow 中Equalify的回答](http://stackoverflow.com/questions/34319008/git-issue-with-visual-studio-2015-update-1)

报错：
><font size=3>Could not open '****.VC.opendb': The process cannot access the file because it is being used by another process.</font>


解决方案：
添加**.VC.opendb*到*.gitignore*文件的*#User-specific files*条目下。

    # User-specific files
    *.suo
    *.user
    *.userosscache
    *.sln.docstates
    *.VC.opendb

本来想复现一下这个错误，结果发现删除掉**.VC.opendb*之后，再打开解决方案，VS居然把*.gitignore*文件也加入了源代码管理里边去……
因为不是第一次遇到这个错误了，就写点东西记下来好了