---
title: Hexo 压缩静态文件
date: 2022-08-27 16:32:22
tags:
    - Hexo
    - Node.js
categories: 教程
---

Hexo 压缩静态文件，优化访问速度。

<!-- more -->

# 1. 安装插件

压缩插件我原来用的是 Hexo-Neat，但是压缩文件会有 `rebuild by neat` 的信息，就换成了以下 3 个插件。
运行以下命令安装。

```shell
pnpm add hexo-html-minifier hexo-clean-css hexo-uglify
```

# 2. 添加配置

在博客目录下 `_config.yml` 添加如下配置。

```yaml
uglify:
    mangle: true
    output:
    compress:
    exclude:
        - "*.min.js"

clean_css:
    exclude:
        - "*.min.css"

html_minifier:
    collapseBooleanAttributes: true
    collapseWhitespace: true
    ignoreCustomComments: [!!js/regexp /^\s*more/]
    removeComments: true
    removeEmptyAttributes: true
    removeScriptTypeAttributes: true
    removeStyleLinkTypeAttributes: true
    minifyJS: true
    minifyCSS: true
```

# 3. 一些问题

主题最好更到最新，不然 Hexo-HTML-Minifier 解析 HTML 比较严格，可能有语法错误。~~例如之前的 ParticleX~~
如果你的主题不能用，应该是语法错了的原因啊。
