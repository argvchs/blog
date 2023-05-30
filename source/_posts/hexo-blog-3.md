---
title: Hexo 博客搭建教程 III
date: 2022-04-17 17:25:34
tags:
    - Hexo
    - JS
    - CSS
categories: 教程
---

书接上文：[Hexo 博客搭建教程 II](/2022/04/17/hexo-blog-2)

<!-- more -->

# 1. 目录介绍

介绍一下博客根目录各文件/文件夹的作用

我的主题用的是 EJS 模板引擎，所以就是 `layout.ejs`

```
blog # Hexo 博客根目录
|---public # 静态网页文件
|---source # 文章
|---themes # 主题
    |---<theme-name>
        |---layout
        |   |---layout.ejs
        |---source # 主题资源文件，里面的内容会生成到静态文件下
```

**下文中的 `source` 均指主题文件夹下的**

# 2. 添加自定义 JS/CSS

在 `source` 下添加自定义文件，把文件放在 `js` `css` 文件夹下分类，不然生成的静态文件会很乱
然后在 `layout.ejs` 下添加如下内容，如果使用网络上的文件直接在 `src` `href` 中填写路径即可

```html
<script src="/js/<file>"></script>
<link rel="stylesheet" href="/css/<file>" />
```

# 3. 一些自定义文件

## 3.1. 鼠标点击特效

```html
<canvas
    id="fireworks"
    style="position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; pointer-events: none; z-index: 32767"
></canvas>
<script src="https://cdn.staticfile.org/animejs/3.2.1/anime.min.js"></script>
<script src="/js/fireworks.min.js"></script>
```

[`fireworks.min.js`](https://static-argvchs.netlify.app/js/fireworks.min.js)

## 3.2. 流星背景特效

```html
<canvas
    id="background"
    style="position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; pointer-events: none; z-index: -1"
></canvas>
<script src="/js/background.min.js"></script>
```

[`background.min.js`](https://static-argvchs.netlify.app/js/background.min.js)

## 3.3. 鼠标指针特效

```html
<div id="cursor"></div>
<link rel="stylesheet" href="/css/cursor.min.css" />
<script src="/js/cursor.min.js"></script>
```

[`cursor.min.css`](https://static-argvchs.netlify.app/css/cursor.min.css) [`cursor.min.js`](https://static-argvchs.netlify.app/js/cursor.min.js)

# 4. Hexo Markdown 语法补充

Markdown 是支持渲染 HTML 的，所以可以实现各种效果
如果你要不使 HTML 标签被渲染可以在右边加 `\` 转义，如 `<tag\>`，但还是推荐 `` `code` `` 的代码格式

## 4.1. 字体

用 `<font>` 元素来实现字体的样式修改

```markdown
<font color=<color> size=<size> face=<face>>...</font>
```

## 4.2. 下载文件

只要把文件放到 `source` 下，在 Markdown 中引用就行

部分文件可能不会下载，直接在浏览器打开，可以用第二种方法

```markdown
[...](file)
<a href="<file>" download>...</a>
```

## 4.3. 注释

Markdown 注释和 HTML 一样

```markdown
<!-- ... -->
```

特别的，用 `<!-- more -->` 可以控制主页预览内容，后面的内容在显示全文时才出现

下一篇：[Hexo 博客搭建教程 IV](/2022/04/17/hexo-blog-4)
