---
title: 评论大清除事件记录
date: 2023-02-19 16:47:28
tags: [评论]
categories: 其他
pin: 1
---

> sry...

用这个文章来记录 Argvchs 的评论大清除

不要误会啊，是因技术原因导致的评论清除

<!-- more -->

## 第一次评论大清除

从 Gitalk 改成 Giscus，懒得把 Issue 转换到 Discussion 了

## 第二次评论大清除

现在我的 Giscus 不用自建服务了，直接用 `data-theme` 参数来引入样式

> 之前是因为 `data-theme` 会出现 CORS 问题，但现在我的 CDN 已经弄好 [Header](https://github.com/argvchs/static/blob/master/netlify.toml) 了，就没有问题

于是我把自建服务的仓库和 `giscus-argvchs[bot]` 都删了

但是由于 Discussion 全部由 `giscus-argvchs[bot]` 创建，删除后全部替换为 [Ghost](https://github.com/ghost)
Giscus 无法搜索由 Ghost 创建的评论，所以评论没了
