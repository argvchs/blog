---
title: Hexo 博客搭建教程 II
date: 2022-04-17 16:02:21
tags:
    - Hexo
    - 主题
categories: 教程
---

书接上文：[Hexo 博客搭建教程 I](/2022/04/17/hexo-blog-1)

<!-- more -->

# 1. 安装主题

首先在[这里](https://hexo.io/themes)选择一个主题。

上面的图片是预览页，下面的蓝色链接是 GitHub 项目页。

选好主题后就要安装，在博客根目录下运行下面的命令将主题 Clone 到本地。

```bash
cd themes
git clone <link>.git <theme> --depth=1
```

> `--depth=1` 是为了 Clone 更快，只 Clone 最新提交。

GitHub 打不开可以用[镜像站](https://hub.njuu.cf)。

例如我的主题是 [ParticleX](https://github.com/theme-particlex/hexo-theme-particlex)，则为：

```bash
git clone https://github.com/theme-particlex/hexo-theme-particlex.git particlex --depth=1
```

安装完成后，在博客根目录下的 `_config.yml` 中设置 theme 参数为你的主题名称，就可以切换主题，一般主题在 GitHub 项目页下都会有介绍和配置说明，可以按照说明自定义页面。

# 2. 创建特殊页面

## 2.1. 分类页

```bash
hexo new page categories
```

打开 `source/categories/index.md`，在 `---` 括起来的地方添加 `type: categories`。

## 2.1. 标签页

```bash
hexo new page tags
```

打开 `source/tags/index.md`，在 `---` 括起来的地方添加 `type: tags`。

## 2.3. 关于页

```bash
hexo new page about
```

打开 `source/about/index.md` 在下面添加内容即可。

---

如果想让标题大写的话可以将 `title` 参数改为大写，例如 `title: About`；
虽然 ParticleX 是根据 `type` 参数来检测的，**但是一些主题是根据 `title` 检测的，可能检测不到**。

# 3. 自定义网站配置

网站配置存放在博客根目录下的 `_config.yml`。

可以看文档了解配置格式：[Hexo 文档](https://hexo.io/docs/configuration.html)。

**P.S.：`titlecase` 参数改变后部分主题可能检测不到 Categories 和 Tags 页面。**

下一篇：[Hexo 博客搭建教程 III](/2022/04/17/hexo-blog-3)
