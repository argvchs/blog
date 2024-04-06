---
title: Hexo-Helper-Crypto
date: 2022-12-08 16:26:33
tags:
    - Hexo
    - 插件
    - CryptoJS
categories: 教程
description: |
    [Hexo-Helper-Crypto](https://github.com/theme-particlex/hexo-helper-crypto) 插件，用于在模板文件内加/解密数据，使用 [CryptoJS](https://github.com/brix/crypto-js)。

    密码是 `123456`。
secret: "123456"
---

[Hexo-Helper-Crypto](https://github.com/theme-particlex/hexo-helper-crypto) 插件，用于在模板文件内加/解密数据，使用 [CryptoJS](https://github.com/brix/crypto-js)。

<!-- more -->

# 1. 安装

```shell
pnpm add hexo-helper-crypto
```

# 2. 使用

在模板文件（以下使用 EJS 模板引擎）中，添加：

```ejs
<% const CryptoJS = crypto(); %>
```

然后可以直接使用 `CryptoJS`，和 [CryptoJS](https://github.com/brix/crypto-js) 接口一样。

以下例子获取了页面标题的 SHA256 值，并用 Base64 编码。

```ejs
<% const CryptoJS = crypto(); %>
<%= CryptoJS.SHA256(page.title).toString(CryptoJS.enc.Base64) %>
```
