---
title: Hexo 博客搭建教程 I
date: 2022-04-17 12:05:13
tags: [Hexo, Git, Node.js]
categories: 教程
---

我搭建这个博客搜了好多教程，都不是特别全，就写了这篇教程

<!-- more -->

## 0. 前言

[Hexo](https://hexo.io) 是一个快速、简洁且高效的博客框架，Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页

Markdown 可以看 GitHub 官方文档：[基本撰写和格式语法](https://docs.github.com/zh/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

## 1. 安装 Git 和 Node.js

-   [Git](https://git-scm.com/downloads)

    完成后用 `git --version` 命令检查，有提示即安装正确

-   [Node.js](https://nodejs.org)

    选择 LTS 或 Current 版本，安装一路确认即可
    完成后用 `node -v` 命令检查，有提示即安装正确

## 2. 启用 Corepack

运行 `corepack enable` 启用 Corepack
启用后自动安装 Yarn 和 PNPM，这样以后的命令都可以换成喜欢的包管理器，我一般用 PNPM

这里是速度参考

![pnpm-vs-npm-vs-yarn](https://pnpm.io/img/benchmarks/alotta-files.svg)

## 3. 安装 Hexo

新建一个文件夹，作为博客目录，`cd` 进入文件夹，运行命令

```bash
pnpm add hexo-cli -g
hexo init --no-install
pnpm i
```

## 4. Hexo 的一些命令

-   生成静态文件：`hexo g`

-   清除静态文件：`hexo cl`

-   在本地运行：`hexo s`

-   部署到网站：`hexo d`

-   生成静态文件并部署到网站：`hexo d -g` 或 `hexo g -d`

-   创建新文章：`hexo new <file>`

**P.S. 创建新文章命令中的 `<file>` 是文件名，标题在文章中的 `title` 参数中修改**

下一篇：[Hexo 博客搭建教程 II](/2022/04/17/hexo-blog-2)
