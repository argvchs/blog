---
title: 搭建 CORS Anywhere
date: 2022-07-04 20:41:42
tags:
    - Gitalk
    - CORS
    - Heroku
categories: 教程
---

Gitalk 官方代理使用 Cloudflare，速度过慢，这里介绍一下自己搭建 CORS Anywhere 代理的过程

<!-- more -->

## 1. 下载项目

打开 [CORS Anywhere](https://github.com/Rob--W/cors-anywhere) 项目地址，点击右上角 Fork 按钮，点 Create Fork，复制到你的仓库
在任意位置输入以下命令，克隆项目到本地，
**`<name>` 是你自己的 GitHub 用户名**

```bash
git clone https://github.com/<name>/cors-anywhere.git && cd cors-anywhere
```

## 2. 注册 Heroku

CORS Anywhere 是在 Heroku 上运行的，所以要注册一下，在[这里](https://signup.heroku.com/)注册

> We could not verify you are not a robot. Please try the CAPTCHA again.

诶？哪有 CAPTCHA？
Heroku 因为用了 Google 的 CHAPCHA 服务，[所以就要](/2022/12/07/fix-github)。。。

GitHub 打不开可以用[镜像站](https://www.library.ac.cn)

重新打开页面，就会出现 CHAPCHA 检测了

## 3. 部署代理

打开 [Heroku](https://www.heroku.com)，点击中间的 Create new app 按钮，输入你喜欢的项目名称，创建项目

下载 [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli)，安装完运行 `heroku -v`检测安装

然后登陆 Heroku CLI，运行 `heroku login -i`，填入你的邮箱和密码
找到你刚才下载 CORS Anywhere 项目的位置，`cd` 到项目根目录，执行以下命令部署

**`<appname>` 是你刚才设置的项目名称**

```bash
git init
heroku git:remote -a <appname>
git add .
git commit -am "first commit"
git push heroku master
```

## 4. 设置黑/白名单

如果你的 CORS 代理被别人得知，用于许多人的 Gitalk 代理中，你的代理就会很卡，这种情况就要设置访问黑/白名单

进入你 Heroku 的项目主页，点击右边的 Settings，找到 Reveal Config Vars 按钮，打开配置变量设置
在左边输入 `CORSANYWHERE_BLACKLIST`（黑名单）或 `CORSANYWHERE_WHITELIST`（白名单），在右边输入你要设置黑/白名单的网站域名，要加上 `http://` 或 `https://` 前缀，用 `,` 分割

**同一个域名要分别用 `http://` 和 `https://` 设置两次，协议不同被视为不同源**

## 5. 修改 Gitalk 设置

部署完代理，就要修改 Gitalk 了，这里给出了两种方法，根据你主题文件夹 `_config.yml` 配置选择

1.  主题有 `gitalk/proxy` 配置
    有这个配置当然最好，将其修改为以下内容

    ```yaml
    gitalk:
        # ...
        proxy: https://<appname>.herokuapp.com/https://github.com/login/oauth/access_token
    ```

2.  没有 `gitalk/proxy` 配置
    没有配置，就要自己修改了，从你主题文件夹下，找出有类似以下内容的文件，**可能细节不太一样**

    ```javascript
    const gitalk = new Gitalk({
        clientID: clientID,
        clientSecret: clientSecret,
        repo: "<%- theme.gitalk.repo %>",
        owner: "<%- theme.gitalk.owner %>",
        admin: ["<%- theme.gitalk.admin %>"],
        language: "<%- theme.gitalk.language %>",
        id: location.pathname,
        distractionFreeMode: false,
    });
    ```

    在 `new Gitalk({...})` 的大括号中添加这一条

    ```javascript
    proxy: "https://<appname>.herokuapp.com/https://github.com/login/oauth/access_token",
    ```

    添加完，你文件的 Gitalk 部分应该类似这样

    ```javascript
    const gitalk = new Gitalk({
        // something...
        proxy: "https://<appname>.herokuapp.com/https://github.com/login/oauth/access_token",
    });
    ```

    这样就配置好了
