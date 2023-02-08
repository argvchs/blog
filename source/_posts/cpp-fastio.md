---
title: C++ Fast-IO
date: 2022-08-11 13:45:19
tags: [C/C++, C++20, Fast-IO]
categories: 算法
---

写了一个 [Fast-IO](https://github.com/argvchs/fast-io) 快读/快写库

支持基本类型与 `__int128_t` 读写，指针地址写入，和 `cin/cout` 用法类似

<!-- more -->

虽然相对于原版函数式 `fread` 快读会有点慢，但还是比 `getchar/putchar` 要快的

Fast-IO 用了 C++20 Concepts，用以下编译参数即可

```bash
g++ <file>.cpp -o <file> -std=c++20 -Wall -O2 -O3 -Ofast
```

## 目录解释

```
fastio.cpp          # 测试文件
fastio.h            # Fast-IO 库源文件
fastio.in           # 输入测试文件
fastio.speed.in     # 速度测试文件
README.md           # README
```

## 使用

-   `using namespace fastio;`

    使用 Fast-IO

-   `using namespace fastio::syms;`

    使用输入输出符号，如 `endl`

-   `rs >> x;`

    读取 x

-   `rs >> x >> y >> z;`

    读取 x, y, z

-   `c = rs.get();`

    读取一个字符到 c

-   `rs.read(x, y, z);`

    读取 x, y, z

-   `x = rs.read<int>();`

    读取一个 `int` 类型的数据到 x

-   `x = rs.read<T>();`

    读取一个 `T` 类型的数据到 x

-   `x = rs.read<char*>(n);` `x = rs.read<const char*>(n);`

    读取一个最长为 n 的字符串到 s，**s 只能为字符指针，不能为数组**

-   `rs >> s;`

    读取一个字符串 s，**s 只能为字符数组，不能为指针**

-   `rs.getline(s, n);`

    读取一行到 s，最多读取 n 个字符

-   `rs.getline(s, n, c);`

    读取字符到 s，最多读取 n 个字符，一直读到 c 停止

-   `rs.ignore();`

    忽略一行

-   `rs.ignore(n);`

    忽略一行，最多忽略 n 个字符（若 n 为 $2147483647$ 则等于 `rs.ignore();`）

-   `rs.ignore(n, c);`

    忽略字符到 c 停止，最多忽略 n 个字符

-   `rs.seek();`

    移动读取指针到开始

-   `rs.eof;`

    rs 是否读到末尾

-   `rs.fail;`

    rs 是否发生错误（读到末尾后，继续读取）

-   `!rs;` `(bool)rs;`

    分别等于 `rs.fail;` `!rs.fail;`

-   `while (rs >> ...);`

    一直读取直到末尾

-   `rs >> bin;` `rs >> oct;` `rs >> dec;` `rs >> hex;`

    按 2 8 10 16 进制读取整数

-   `rs >> skipws;`

    忽略前导空格

-   `rs.setbase(base);`

    按 base 进制读取整数，超出范围默认 10 进制 $(2 \le base \le 36)$

-   `rs >> reset;`

    取消前面的所有设置

-   `ws << x;`

    写入 x

-   `ws << x << y << z;`

    写入 x, y, z

-   `ws.put(c);`

    写入一个字符 c

-   `ws.write(x, y, z);`

    写入 x, y, z

-   `ws.flush();` 或 `ws << flush;`

    刷新流

-   `ws << endl;`

    写入换行

-   `ws << ends;`

    写入空格

-   `ws << boolalpha;`

    设置写入 `bool` 时用 `true/false`

-   `ws << noboolalpha;`

    设置写入 `bool` 时用 `0/1`

-   `ws << showpos;`

    设置写入非负数（不包括 `bool`）时前面加 `+` 号

-   `ws << noshowpos;`

    设置写入非负数（不包括 `bool`）时前面不加 `+` 号

-   `ws << showpoint;`

    设置写入浮点数时严格保留 `setprecision` 时设置的位数

-   `ws << noshowpoint;`

    设置写入浮点数时不严格保留 `setprecision` 时设置的位数

-   `ws << bin;` `ws << oct;` `ws << dec;` `ws << hex;`

    按 2/8/10/16 进制写入整数

-   `ws << lowercase;`

    按大于 10 的进制写入整数时，字母大写（默认小写）

-   `ws << uppercase;`

    按大于 10 的进制写入整数时，字母小写（默认小写）

-   `ws << showbase;`

    写入 8/16 进制的整数时，在前面显示 `0`/`0x`

-   `ws << noshowbase;`

    写入 8/16 进制的整数时，不在前面显示 `0`/`0x`

-   `ws << setbase(base);`

    按 base 进制写入整数，超出范围默认 10 进制 $(2 \le base \le 36)$

-   `ws << unitbuf;`

    设置每写入一个数据就刷新流

-   `ws << nounitbuf;`

    设置超过最大限制 SIZ 时才刷新流（SIZ 为一个 `const` 变量）

-   `ws << setw(width);`

    设置下一次写入宽度若小于 `width`，就填补字符（下一次写入重置）

-   `ws << setfill(c);`

    设置 `setw` 填补的字符，默认为空格

-   `ws << setprecision(precision);`

    设置浮点数保留位数，默认保留 3 位

-   `ws << reset;`

    取消前面的所有设置

-   `rstream rs;`

    创建读流（已经有默认流 rs 了，会发生错误）

-   `wstream ws;`

    创建写流（已经有默认流 ws 了，会发生错误）

-   `rfstream rfs(dir);`

    创建文件读流，从 dir 路径文件读取（也可以是 `FILE*` 文件指针），和普通读流用法相同

-   `wfstream wfs(dir);`

    创建文件写流，写入 dir 路径的文件（也可以是 `FILE*` 文件指针），和普通写流用法相同

-   `sstream ss;`

    创建字符串流，可读写，读取后不会删除数据，会移动读取指针

-   `ss.str();`

    获取字符串流的数据

-   `ss.str(s);`

    将字符串流的数据替换为 s 并移动读取指针到开始

## 接口

-   重载运算符

    **注意要用 `fastio::interface::rstream` `fastio::interface::wstream` 来重载**

    以下是一些示例程序

    ```cpp
    // overload read/write for std::string
    auto &operator<<(fastio::interface::rstream &rs, string &s) {
        static char buf[1005];
        rs >> buf;
        s = buf;
        return rs;
    }
    auto &operator<<(fastio::interface::wstream &ws, const string s) { return ws << s.c_str(); }

    // overload write for punctuation
    enum punctuation { comma, simicolon, fullstop, question, exclamatory };
    auto &operator<<(fastio::interface::wstream& ws, const punctuation s) {
        if (s == comma) ws.put(',');
        else if (s == simicolon) ws.put(';');
        else if (s == fullstop) ws.put('.');
        else if (s == question) ws.put('?');
        else if (s == exclamatory) ws.put('!');
        return rs;
    }

    // overload read/write for std::vector<T>
    template<class T> auto& operator<<(fastio::interface::rstream& rs, const vector<T>& v) {
        v.clear();
        T x;
        int n = rs.read<size_t>();
        while (n--) {
            rs >> x;
            v.push_back(x);
        }
        return ws;
    }
    template<class T> auto& operator<<(fastio::interface::wstream& ws, const vector<T> v) {
        for (T x : v) ws << x << ' ';
        return ws;
    }
    ```
