---
title: EasyPYTool 使用说明
date: 2022-07-06 15:47:11
tags: [Python, PIP]
categories: 工具
---

[EasyPYTool](https://github.com/argvchs/easypytool) 是一个 **Windows** 上简单 & 轻量级的 Python 环境配置工具

<!-- more -->

~~毕竟那些用 Linux 的**神犇**绝对能自己处理好这些环境配置的~~

> 仅 5 个 Bat 文件，总占用空间 < `5KB`

## 文件解释

-   `mirror.set.bat`

    设置 Python 镜像源和代理，镜像源默认 [Tuna](https://pypi.tuna.tsinghua.edu.cn/simple)，代理默认不设置

-   `mirror.unset.bat`

    重置 Python 镜像源和 Proxy

-   `pack.export.bat`

    导出 PIP 包，存储到`packages`文件夹，可能需要一定时间

-   `pack.import.bat`

    离线安装导出的 PIP 包, 可以将此程序放在 U 盘/移动硬盘上，完成两个电脑间的包转移

-   `pysetup.bat`

    安装 Python，从 [Huawei Cloud](https://repo.huaweicloud.com/python) 加速下载，仅支持稳定版

-   `clearcache.bat`

    清理缓存（导出的 PIP 包和 Python 安装文件）

#### 只有这些了
