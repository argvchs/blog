---
title: 线性化提交历史
date: 2023-02-26 08:47:56
tags: [Git, GitHub]
categories: 其他
---

ParticleX 主题之前用了 Git Flow AVH，提交记录很丑

这篇文章说一下怎么线性化提交历史

<!-- more -->

## 1. 线性化

其实这样用 `rebase --root` 就可以线性化了

如果原分支不是 `master` 的话要把下面的都改一下，**新建一个分支是因为操作很危险**

```bash
git checkout master
git checkout -b new
git rebase --root
```

过程中可能会有冲突出现，处理好冲突然后继续运行

```bash
git commit --no-edit
git rebase --continue
```

最后推送分支，打开 GitHub 的 Insight 就会发现，已经变成线性提交记录啦

```bash
git checkout master
git reset new
git branch -D new
git push -f
```

## 2. 扩展

如果分支历史上有**很多** Tag 的话要**把所有 Tag 全部清除**，然后手动添加

> 如果没有**很多** Tag 可以单个删除

```bash
git push origin --delete $(git tag -l)
git tag -d $(git tag -l)
```

---

如果一个 `custom` 分支依赖 `master`，那可以用 `merge --squash`

```bash
git checkout master
git checkout -b new
git merge --squash --allow-unrelated-histories custom
```

过程中可能也会有冲突出现，处理好冲突就提交推送

```bash
git commit --no-edit
git checkout custom
git reset new
git branch -D new
git push -f
```

## 3. 后言

ParticleX 是无法做到完全线性提交的，因为有 `custom` 分支一直合并

其实有一个问题就是 GitHub 记录提交时间可能有错，我在本地 `git show` 查看日期是旧的没有改变，但是 GitHub 上日期就变成刚提交的了，就这样吧
