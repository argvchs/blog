---
title: Hexo-Babel
date: 2022-12-13 15:51:22
tags:
    - Hexo
    - 插件
    - Babel
categories: 工具
---

[Hexo-Babel](https://github.com/argvchs/hexo-babel) 插件，使用 Babel 编译转换 JS 文件

<!-- more -->

## 安装

```bash
pnpm add hexo-babel
```

## 配置

```yaml
babel:
    options:
    exclude:
        - "*.min.js"
```

`options` 详见 [Options · Babel](https://babel.dev/docs/en/options) 和 [@babel/preset-env · Babel](https://babel.dev/docs/en/babel-preset-env#options)

例如这是一种配置（要先安装 `@babel/preset-env`）

```bash
pnpm add @babel/core @babel/preset-env -D
```

```yaml
babel:
    options:
        presets:
            - - "@babel/preset-env"
              - targets: last 5 versions, not dead, > 0.3%
        sourceType: script
    exclude:
        - "*.min.js"
```

或者不填 `options` 参数，使用 `babel.config.json`

```json
{
    "presets": [
        [
            "@babel/preset-env",
            {
                "targets": "last 5 versions, not dead, > 0.3%"
            }
        ]
    ],
    "sourceType": "script"
}
```
