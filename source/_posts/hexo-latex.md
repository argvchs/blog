---
title: Hexo 博客使用 LaTeX
date: 2022-06-17 22:48:06
tags:
    - Hexo
    - LaTeX
categories: 教程
---

$$
\begin{aligned}
\alpha_0&=\mathop{\arg\min}\limits_{\alpha_0}f(x^0-\alpha\nabla f(x^0))\\
&=\mathop{\arg\min}\limits_{\alpha_0\geq 0}(0+(2+2\alpha-3)^2+4(-1-1024\alpha+5)^4)\\
&=\mathop{\arg\min}\limits_{\alpha_0\geq 0}\phi(\alpha)
\end{aligned}
$$

<!-- more -->

# 0. 前言

众所周知，Hexo 是不自带 $\LaTeX$ 的，所以我们就要让 Hexo 支持 $\LaTeX$。

网上很大一部分文章都是介绍 Kramed 渲染器的，可我的博客总是无法正确显示，就写了这篇文章。

> 如果你正在使用 [ParticleX 主题](/2022/05/10/hexo-theme-particlex)，可以忽略 MathJax 的内容，因为主题内置了 $\KaTeX$。
>
> 但是 Pandoc 渲染器还是很好的。

# 1. 安装环境

由于 Kramed 渲染总会出错，我们这里选择用 Pandoc 渲染。
先**下载** [Pandoc](https://pandoc.org/installing.html) 到本地，安装一路确认即可。

在根目录下执行以下命令，删除默认渲染器。

```bash
pnpm rm hexo-renderer-marked
```

安装 Pandoc 和 MathJax。

```bash
pnpm add hexo-renderer-pandoc hexo-filter-mathjax
```

# 2. 配置 Pandoc 和 MathJax

打开根目录下 `_config.yml`，添加如下配置：

```yaml
pandoc:
    extra:
        - no-highlight:
    extensions:
        - +abbreviations
        - +autolink_bare_uris
        - +emoji
        - +hard_line_breaks
        - -implicit_figures
        - +mark
        - +short_subsuperscripts

mathjax:
    tags: none # or 'ams' or 'all'
    single_dollars: true # enable single dollar signs as in-line math delimiters
    cjk_width: 0.9 # relative CJK char width
    normal_width: 0.6 # relative normal (monospace) width
    append_css: true # add CSS to pages rendered by MathJax
    every_page: true # if true, every page will be rendered by MathJax regardless the `mathjax` setting in Front-matter
    extension_options:
        {}
        # you can put your extension options here
        # see http://docs.mathjax.org/en/latest/options/input/tex.html#tex-extension-options for more detail
```

配置完就可以使用 $\LaTeX$ 了。
