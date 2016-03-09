---
title: powershell和cmake
date: 2016-03-09 18:18:03
categories: windows
tags:
---

在powershell环境下安装cmake，并用cmake生成metis。

<!--more-->


**问题描述和絮絮叨叨**
今天遇到了个问题，老师提出来要把metis在windows下边编译为x64的。

metis在最新版本5.1.0里边是提供windows版本的生成方式的。遗憾的是我之前安装cmake并在图形界面安装之后，调试了半天才只能搞定32位的编译环境。今天逼不得已了，回头去看了看metis的build文件，看到里边提供了两种方式，一种是cmake GUI，另一种是cmake command line。索性试一试第二种。

首先试了一下，发现虽然之前装了cmake GUI，但是还要再重新装一下cmake command line才可以在命令行下使用。恰好看到powershell好像还挺好用，就在powershell环境下安装了一下cmake。安装过程其实有点恼人啊，因为不熟悉powershell嘛。


**解决方案**

* 在powershell中安装cmake：

 * 这个过程中需要使用[chocolatey](https://chocolatey.org/)来作为powershell的“apt-get”，安装方法就按照官网的来就好。要注意在powershell中，Get-ExecutionPolicy至少为Bypass才可以。
 * 之后安装[chocolatey cmake](https://chocolatey.org/packages/cmake)，安装完之后发现并没有自动更新PATH，所以又安装的cmake.portable。

OK，现在在powershell中敲一下cmake就发现可以用啦。

* 使用cmake编译metis：

 * 其实这个事超简单，完成上边的事情之后，转到metis的目录下按照说明cmake了一下，DONE！
 * 不过有个事吧，就是visual studio 2015有个支持git进行源代码管理的功能，但是呢，cmake metis之后，sln、vcxproj这些项目文件都是在metis的子目录里边，这个时候想在VS中把代码添加到源代码管理就出问题了，因为貌似VS暂时只支持把sln文件所在的目录中包含的源代码添加到源码控制中。
 * 为此，特地改了一下metis的vsgen文件，重新制定让他把这些项目文件直接生成到metis的根目录下。这样虽然根目录稍微有点乱，但是至少有源代码控制之后，再写代码就很爽了。

今天就说这些吧。