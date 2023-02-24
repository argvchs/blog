---
title: 安装 MinGW-w64
date: 2022-07-21 22:03:08
tags: [C/C++, MinGW, GCC]
categories: 工具
---

MinGW-w64 安装教程

<!-- more -->

## 0. 前言

看了好多 MinGW-w64 安装教程，都是从 SourceForge 上下载，版本很旧，C++17/C++20 一些 STL 库还没更新，不能用万能头，就很难受啊，这篇文章教你如何找到最新 MinGW-w64 版本

## 2. 找到 MinGW-w64

打开 https://www.mingw-w64.org/downloads

![mingw-w64-download](https://static-argvchs.netlify.app/images/mingw-w64-download.png)

如果你按照网上大部分教程的描述，找到 [SourceForge](http://sourceforge.net/projects/mingw-w64/files/mingw-w64/)，就会显示如下

虽然最新版本是 v10.0.0，可那是源码，最新构建版本是 v8.1.0，太旧了

## 3. 最新版本

其实，如果你仔细看一看，就会发现上面有一个 [MinGW-Builds](https://github.com/niXman/mingw-builds-binaries/releases)，但因为描述太少被忽略了
看一下版本：Release 12.1.0-rt_v10-rev3，WC 这么新，往下翻

![mingw-builds](https://static-argvchs.netlify.app/images/mingw-builds.png)

竟然还有构建版本！
**这里 `i686` 是 32 位版本，`x86_64` 是 64 位版本，`seh` 和 `dwarf` 性能更好，比 `sjlj` 要快一些 **
下载完，解压缩一下，然后把里面的 `bin` 文件夹添加到环境变量即可
