---
title: 评论清除事件记录
date: 2023-02-19 16:47:28
tags:
    - 评论
categories: 其他
---

用这个文章来记录 Argvchs 的评论清除事件。
不要误会啊，是技术原因导致的，我没有评论审查。

<!-- more -->

## 第 1 次评论清除

从 Gitalk 改成 giscus，懒得把 Issue 转换到 Discussion 了。

## 第 2 次评论清除

现在我的 giscus 不用自建服务了，直接用 `data-theme` 参数来引入自定义样式。

> 之前不用上述参数，是因为会出现 CORS 问题，但现在我的 CDN 已经弄好 [Header](https://github.com/argvchs/static/blob/master/netlify.toml) 就没有问题啦。

于是我把自建服务的仓库和对应 Github App `giscus-argvchs` 都删了。

但是由于 Discussion 全部由 `giscus-argvchs` 创建，删除后全部替换为 [`ghost`](https://github.com/ghost) 帐号了。

可是 giscus 无法搜索由 ghost 创建的评论啊，所以就没了。
