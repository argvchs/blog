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

介绍一下博客根目录各文件/文件夹的作用，我的主题用的是 EJS，其他如 Pug/Jade 等和原始 HTML 相差太大的模板引擎请不要参考本篇 ~~我太懒了~~

```
<root>
|---public # 静态网页文件
|---source # 文章
|---themes # 主题
    |---<theme-name>
        |---layout # 布局文件
        |   |---layout.ejs # 网页的基本布局
        |---source # 主题资源文件，里面的内容会生成到静态文件下
```

**下文中的 `source` 均指主题文件夹下的**

# 2. 添加自定义 JS/CSS

在 `source` 下添加自定义文件，把文件放在 `js` `css` 文件夹下分类，不然生成的静态文件会很乱
然后在 `layout.ejs` 下添加如下内容，如果使用网络上的文件直接在 `src` `href` 中填写路径即可

**`<file>` 为自定义文件名称**

```html
<script src="/js/<file>"></script>
<link rel="stylesheet" href="/css/<file>" />
```

# 3. 我用的自定义文件

## 3.1 `live2d.min.js`：Live2D 组件，需要 PIXI.js

**已被弃用了，因为写的太乱并且很卡**

使用：

将[这里](https://github.com/imuncle/live2d)的 Live2D 模型 Clone 到本地，选择一个模型（是 Cubism 3 版本的，在 `live2d_3` 文件夹下）复制到 `source/model`
**`<model-name>` 为模型名称，参数和我给的 CSS 样式可以更改，以下是我的配置**

```html
<div id="L2dCanvas"></div>
<link rel="stylesheet" href="/css/live2d.min.css" />
<script src="https://cdn.staticfile.org/pixi.js/4.6.1/pixi.min.js"></script>
<script src="/js/live2d.min.js"></script>
<script>
    var v = new Viewer({
        width: 240,
        height: 325,
        right: "0",
        bottom: "0",
        basePath: "/model",
        role: "<model-name>",
        mobile: true,
    });
</script>
```

下载：
-   [`live2d.min.js`](https://static-argvchs.netlify.app/js/live2d.min.js)
-   [`live2d.min.css`](https://static-argvchs.netlify.app/css/live2d.min.css)
-   [`live2d.zip`](https://static-argvchs.netlify.app/assets/model.zip)

## 3.2 `fireworks.js`：鼠标点击特效，需要 Anime.js

使用：

```html
<canvas
    id="fireworks"
    style="position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; pointer-events: none; z-index: 32767"
></canvas>
<script src="https://cdn.staticfile.org/animejs/3.2.1/anime.min.js"></script>
<script src="/js/fireworks.min.js"></script>
```

下载：
-   [`fireworks.min.js`](https://static-argvchs.netlify.app/js/fireworks.min.js)

## 3.3 `background.js`：流星背景特效

使用：

```html
<canvas
    id="background"
    style="position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; pointer-events: none; z-index: -1"
></canvas>
<script src="/js/background.min.js"></script>
```

下载：
-   [`background.min.js`](https://static-argvchs.netlify.app/js/background.min.js)

## 3.4 `cursor.js`：鼠标指针特效

使用：

```html
<div id="cursor"></div>
<link rel="stylesheet" href="/css/cursor.min.css" />
<script src="/js/cursor.min.js"></script>
```

下载：
-   [`cursor.min.css`](https://static-argvchs.netlify.app/css/cursor.min.css)
-   [`cursor.min.js`](https://static-argvchs.netlify.app/js/cursor.min.js)

# 4. Hexo Markdown 语法补充

Markdown 是支持渲染 HTML 的，所以可以实现各种效果
如果你要不使 HTML 标签被渲染可以在右边加 `\` 转义，如 `<tag\>`，但还是推荐 `` `code` `` 的代码格式

## 4.1 字体

用 `<font>` 来实现字体的样式修改

**`<color>` `<size>` `<face>` 分别是你字体的颜色，大小和字体名称**

```markdown
<font color=<color> size=<size> face=<face>>Text...</font>
```

## 4.2 下载文件

Markdown 下载文件，网上搜到的都是 `post_asset_folder` 这个参数~~（也不知道为什么我不能用）~~

只要把文件放到 `source` 下，在 Markdown 中引用就行
部分文件可能不会下载，在浏览器打开，如果有洁癖可以用第二种方法

```markdown
[Download](file)
<a href="<file>" download>Download this file.</a>
```

## 4.3 注释

Markdown 注释和 HTML 一样

```markdown
<!-- ... -->
```

特别的，用 `<!-- more -->` 可以控制主页预览内容，后面的内容在显示全文时才出现

## 4.4 解决部分主题没有块引用的样式

~~例如 Particle~~

块引用会解析成 `<blockquote>` 标签，添加自定义 CSS 即可

下一篇：[Hexo 博客搭建教程 IV](/2022/04/17/hexo-blog-4)
