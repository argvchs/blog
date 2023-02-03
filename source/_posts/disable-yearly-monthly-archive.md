---
title: 禁用年度月度归档
date: 2023-01-05 17:53:55
tags: Hexo
categories: 其他
---

Hexo 会自动生成年度月度归档，可是 ParticleX 主题没有这个功能 ~~我太懒了~~

所以我们就要禁用！

<!-- more -->

Hexo 是使用 [Hexo-Generator-Archive](https://github.com/hexojs/hexo-generator-archive) 生成归档的，在根目录 `_config.yml` 添加这些，即可禁用

```yaml
archive_generator:
    enabled: true
    per_page: 0
    yearly: false
    monthly: false
    daily: false
```
