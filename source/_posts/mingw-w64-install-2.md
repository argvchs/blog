---
title: 安装 MinGW-w64 II
date: 2023-06-24 09:28:06
tags:
    - C/C++
    - MinGW
    - GCC
    - Clang
categories: 教程
---

突然发现可以安装 GCC 的时候顺带安装 Clang，于是又写了一篇。

上一篇是这个：[安装 MinGW-w64](/2022/07/21/mingw-w64-install)

<!-- more -->

再次打开这个链接 https://www.mingw-w64.org/downloads，在下面似乎多了一个 [WinLibs.com](https://winlibs.com)。

![winlibs](https://static-argvchs.netlify.app/images/winlibs.png)

在下面找到 Download 就可以下载了，我一般选择以下这种格式的。

```
GCC ... (with POSIX threads) + LLVM/Clang/LLD/LLDB ... + MinGW-w64 (UCRT) - release ... (LATEST)
```

和上一篇一样，解压到一个适合的位置，然后把里面的 `bin` 文件夹添加到环境变量即可。
