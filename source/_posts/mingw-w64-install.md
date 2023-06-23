---
title: 安装 MinGW-w64
date: 2022-07-21 22:03:08
tags:
    - C/C++
    - MinGW
    - GCC
categories: 教程
---

看了好多 MinGW-w64 安装教程，都是从 SourceForge 上下载，版本很旧，甚至不能用万能头，就很难受啊

这篇文章教你如何找到最新 MinGW-w64 版本

<!-- more -->

# 2. 找到 MinGW-w64

打开 https://www.mingw-w64.org/downloads

![mingw-w64-download](https://static-argvchs.netlify.app/images/mingw-w64-download.png)

如果你按照网上大部分教程的描述，就会找到 [SourceForge](http://sourceforge.net/projects/mingw-w64/files/mingw-w64)

虽然最新版本是 v10.0.0，可那是源码，最新构建版本是 v8.1.0，太旧了

# 3. 最新版本

其实如果仔细看一下，就可以发现上面有一个 [MinGW-Builds](https://github.com/niXman/mingw-builds-binaries/releases)，但因为描述太少被忽略了

![mingw-builds](https://static-argvchs.netlify.app/images/mingw-builds.png)

我一般会选带有 `posix-seh-ucrt` 的

解压到一个适合的位置，然后把里面的 `bin` 文件夹添加到环境变量即可
