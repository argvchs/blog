---
title: MSYS2 安装 Clang
date: 2022-09-10 12:22:17
tags: [C/C++, MSYS2, GCC, Clang]
categories: 工具
---

使用 MSYS2 安装 Clang 的教程

<!-- more -->

## 1. 安装 MSYS2

<https://www.msys2.org/#installation>

一路确认即可

## 2. 打开 MSYS2 Shell

MSYS2 安装完成后开始菜单一般会有 MSYS2 32/64 bit 文件夹，运行里面的 MSYS2 MSYS

如果没有就记住之前的安装路径（以下的 `<msys2-dir>`），用以下命令打开 MSYS2 Shell

```bash
<msys2-dir>/msys2_shell -msys
```

## 3. 安装 Clang

MSYS2 使用 Pacman 作为包管理器，首先要更新一下软件包（用 MSYS2 Shell）

```bash
pacman -Sy
pacman -Su
```

运行完之后会关闭，重新打开 MSYS2 Shell 再输入一遍 `pacman -Su` 即可
然后运行以下命令安装 Clang

```bash
pacman -S mingw64/mingw-w64-x86_64-make mingw64/mingw-w64-x86_64-gdb mingw64/mingw-w64-x86_64-clang
```

然后把 `<msys2-dir>/mingw64/bin` 添加到环境变量即可
**注意要添加到用户变量，不然 MSYS2 可能造成环境变量污染**
