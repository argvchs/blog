---
title: GFonts-Helper 使用说明
date: 2022-07-25 13:29:33
tags: 字体
categories: 工具
---

[GFonts-Helper](https://github.com/argvchs/gfonts-helper) 是一个下载并压缩 Google Fonts 的工具

<!-- more -->

## 1. 安装

```bash
pnpm add gfonts-helper -g
```

## 2. 使用

```bash
gfonts-helper <url> <group>
```

`<url>` 是 Google Fonts API 的 URL

`<group>` 是分组下载的每组数量，因为一次下载可能最后会卡住，默认为 20

e.g.

```bash
gfonts-helper "https://fonts.googleapis.com/css2?family=Roboto&display=swap"
gfonts-helper "https://fonts.loli.net/css2?family=Roboto&display=swap"
gfonts-helper "https://fonts.geekzu.org/css2?family=Roboto&display=swap"
```

还可以换成缩写

```bash
gfhelper <url> <group>
```

运行完生成 `fonts.min.css` 一个文件，和 `fonts` 一个文件夹
