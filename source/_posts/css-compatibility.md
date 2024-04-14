---
title: Hexo 自动处理 CSS 兼容性
date: 2022-12-12 14:22:40
tags:
    - Hexo
    - CSS
categories: 教程
---

CSS 兼容性太麻烦了，所以要自动处理。

<!-- more -->

# 1. 安装插件

Hexo-Autoprefixer 可以自动处理 CSS 兼容性。

```bash
pnpm add hexo-autoprefixer
```

# 2. 配置

`_config.yml`

```yaml
autoprefixer:
    exclude:
        - "*.min.css"
```

`.browserslistrc`

```browserslistrc
last 5 versions, not dead, > 0.3%
```

上面的 Browserslist 是我的配置，更详细的可以看[这里](https://github.com/browserslist/browserslist#config-file)。
