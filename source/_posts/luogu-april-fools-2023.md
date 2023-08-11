---
title: 2023 年洛谷愚人节比赛
date: 2023-04-09 18:19:08
tags:
    - 洛谷
categories: OI
---

2023 年洛谷愚人节比赛，我竟然拿到 #4 了。

<!-- more -->

以下是部分题的题解。

# A. Mon ami

_The ciphertext is Styles._

直接得出答案为 `Styles`。

# B. 之后就一个人都没有了吗？

打开之后发现是一张 SVG 格式的空白图片，图片内容应该是隐藏了。

于是用 SVG Path Editor 查看，得出答案：`flag{YouReallyFoundTheSentence}`，去掉 `flag` 即为 `YouReallyFoundTheSentence`。

# C. 一万巫女

输出 10001 个硬币即可，注意输出格式，多试几次就能过了。

# F. 14 Understand Variants

[查看 GitHub 源码](https://github.com/LuoguAprilFoolTeam/14-Understand-Variants)，得出规律，然后根据规律做即可。

注意 Time 的题，要在规定时间提交。

# I. 洛谷管理全真体验 III

不太好判断，按测试点分为 4 5 6 三组，然后试答案即可。

# M. 挑战

暴力拿到 6 分。

按照题目要求，用类似 Base64 格式读取，使用 `__int128_t` 存储数字，还要注意空间复杂度。

# P. 宇宙的终极奥秘

这个游戏玩到永恒就可以发现时间研究最底下有一个 _点我获得答案_。

如果玩完这个游戏，时间就太长了，于是直接搜索一个[已经玩完的存档](https://gist.github.com/keybounce/e565b75e897e200d17f271f25f480762)，然后算出答案。

# Q. 困境

## Subtask 1

`right` `left` 即可找到 `escape` 文件，有提示信息。

## Subtask 2

能找到一个 `escape` 文件，并且发现其他每个文件里都有一串字符。

找到内容是 `escape` 的文件；
找到内容是内容是 `escape` 的文件的文件名的文件；
找到内容是内容是内容是 `escape` 的文件的文件名的文件的文件名的文件……

依此类推，再在前面加上 `start`，答案即为 `start...escape`。

---

致谢名单：

-   [@yr317430_xht](https://www.luogu.com.cn/user/959024)：OPQS 题 133 分换 CDGH 题 400 分。

-   [@rainygame](https://www.luogu.com.cn/user/804607)：P 题 100 分换 J 题 55 分。

-   [@qidirj](https://www.luogu.com.cn/user/371468)：J 题 50 分换 Q 题 33 分。

-   [@trh0630](https://www.luogu.com.cn/user/252093)：BDG 题 300 分换 J 题 67 分。

-   [@Jasoncwx](https://www.luogu.com.cn/user/592684)：FJPQ 题 333 分换 OS 题 115 分。

-   [@MornEveGlow](https://www.luogu.com.cn/user/52914)：P 题 100 分换 O 题 55 分。

-   [@蔡竣凯](https://www.luogu.com.cn/user/341036)：O 题 55 分换 E 题 100 分。
