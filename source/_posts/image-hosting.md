---
title: 搭建图床
date: 2022-11-18 16:06:43
tags:
    - 图床
    - Netlify
categories: 教程
---

之前图床用的是 [ImgTP](https://www.imgtp.com)，因为能传 SVG，当初就选了这个，但现在总是间歇性的打不开了。
还是自建图床吧。

<!-- more -->

# 1. 安装 PicGo

我们用 [PicGo](https://github.com/Molunerfinn/PicGo/releases) + GitHub 方式来自建图床。

# 2. 创建仓库

应该都会创建吧，注意一定要是 Public 仓库，还要加一个 README。

> Initialize this repository with a README.

# 3. 创建 Token

从[这里](https://github.com/settings/tokens/new)创建 Token。

GitHub 已经有 Fine-grained Token 了，但不能永久使用啊，所以还是用普通 Token。

![create-token-for-upload-images](https://static-argvchs.netlify.app/images/create-token-for-upload-images.png)

创建完后会提示你复制 Token，记下来以后要用到。

# 4. 配置 PicGo

打开 PicGo，找到图床设置。

![picgo](https://static-argvchs.netlify.app/images/picgo.png)

注意分支名，如果你没设置默认分支为 `master` 的话就改成 `main`。

# 5. Netlify 加速

GitHub 太慢了，我们需要用 [Netlify](https://netlify.com) 加速一下。

我太懒就不说了，和加速 Github Pages 一样；
可以依照[之前的文章](/2022/04/17/hexo-blog-4/)设置一下。

做完之后，把 PicGo 复制下的链接这样修改一下即可。~~突然发现还可以缩短链接~~

```
https://raw.githubusercontent.com/<user>/<repo>/<branch>/<image>
>>>
https://<domain>.netlify.app/<image>
```
