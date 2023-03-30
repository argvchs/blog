---
title: Hexo 博客搭建教程 IV
date: 2022-04-17 18:37:18
tags:
    - Hexo
    - GitHub
    - Netlify
    - Vercel
categories: 教程
---

书接上文：[Hexo 博客搭建教程 III](/2022/04/17/hexo-blog-3)

<!-- more -->

## 1. 配置 SSH 密钥

首先要有一个 [GitHub](https://github.com) 帐号

**`<user>` 和 `<email>` 分别是你自己的 GitHub 用户名和注册时使用的邮箱**

注册完成后回到主页，点击左边的 New 新建仓库，名称为 `<user>.github.io`，然后点击 Create repositpory 完成创建

在命令行输入命令，获取 SSH 密钥，这个过程会提示你输入一些东西，一直回车就行了

```bash
ssh-keygen -t ed25519 -C <email>
```

然后添加到 SSH-Agent

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

输入以下命令复制 SSH 密钥，先不用管，后面会用到

```bash
clip < ~/.ssh/id_ed25519.pub
```

如果你用 Windows CMD

```batch
clip < %USERPROFILE%\.ssh\id_ed25519.pub
```

打开你 GitHub 右上角的头像中的 Settings 设置，点击左边的 SSH and GPG keys，点击右上角的 New SSH key，将 SSH 密钥复制到 Key 中，Title 不用写，点击 Add SSH key 添加密钥

设置好 SSH 密钥后用 `ssh -T git@github.com` 检测，如果出现 `Hi! You've successfully authenticated` 则配置成功

## 2. 更改默认分支（可选）

默认分支以前是 `master`，现在改成了 `main`
网上搜到关于 GitHub 的文章，大部分默认分支都是 `master`

打开 https://github.com/settings/repositories

第一个输入框就是你的默认分支，更改后点击 Update 即可

也可以不更改，但以后的操作都要改成 `main`

## 3. 部署到 GitHub Pages

使用下面的命令初始配置

```bash
git config --global user.name "<user>"
git config --global user.email "<email>"
```

打开你博客根目录的 `_config.yml`，设置参数

```yaml
url: https://<user>.github.io/
deploy:
    type: git
    repo: git@github.com:<user>/<user>.github.io.git
    branch: master
    message:
```

设置好参数，使用下面的命令安装部署插件，安装了才能部署到 GitHub Pages

```bash
pnpm add hexo-deployer-git
```

在博客根目录下使用 `hexo d -g` 部署到 GitHub Pages

## 4. 部署到 Vercel 或 Netlify 加速访问

-   Vercel

    先注册一个 [Vercel](https://vercel.com/login) 帐号，通过 GitHub 注册

    注册成功后跳转到你的首页，点击 New project，跳转后在 Import Git Repository 中选择你的 Hexo 博客，跳转后点击 Deploy 上传到 Vercel

    上传完成点击 Goto Dashboard 来到项目主页，选择顶部的 Settings，在 Project Name 中更改你网站的名称

-   Netlify

    先注册一个 [Netlify](https://app.netlify.com/) 帐号，通过 GitHub 注册

    注册成功后跳转到你的首页，点击 Add new site 中的 Import an existing project，点击 GitHub，与 GitHub 关联

    关联 GitHub 后在下面会出现你 GitHub 中的仓库，点击你创建的 Hexo 博客，再点击 Deploy site 上传

    上传完成会跳转到项目主页，选择 Site settings，跳转后往下滑，点击 Change site name 更改你网站的名称
