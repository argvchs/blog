---
title: C++ Fast-IO
date: 2022-08-11 13:45:19
tags:
    - C/C++
    - C++20
    - Fast-IO
categories: 算法
---

写了一个 [Fast-IO](https://github.com/argvchs/fast-io) 快读快写库

支持基本类型读写，指针地址写入，和 `cin` `cout` 用法类似

<!-- more -->

虽然相对于原版函数式 `fread` 快读会有点慢，但还是比 `getchar` `putchar` 要快的

Fast-IO 用了 C++20，用以下编译参数即可

```bash
g++ <file>.cpp -o <file> -std=c++20 -Wall
```

# 1. 目录解释

```
fastio.cpp          # 测试代码
fastio.h            # Fast-IO 库源代码
fastio.in           # 输入测试数据
fastio.speed.in     # 速度测试数据
README.md           # README
```

# 2. 使用

-   `using namespace fastio;`

    使用 Fast-IO

-   `using namespace fastio::symbols;`

    使用输入输出符号，如 `endl`

-   `is >> x;`

    读取 `x`

-   `is >> x >> y >> z;`

    读取 `x` `y` `z`

-   `c = is.get();`

    读取一个字符到 `c`

-   `is.read(x, y, z);`

    读取 `x` `y` `z`

-   `x = is.read<int>();`

    读取一个 `int` 类型的数据到 `x`

-   `x = is.read<T>();`

    读取一个 `T` 类型的数据到 `x`

-   `is >> s;`

    读取一个字符串 `s`，**s 只能为字符数组，不能为指针**

-   `is.getline(s);`

    读取一行到 `s`，**s 只能为字符数组，不能为指针**

-   `is.getline(s, end);`

    读取字符到 `s`，一直读到 `end` 停止，**s 只能为字符数组，不能为指针**

-   `is.ignore();`

    忽略一行

-   `is.ignore(end);`

    忽略字符到 c 停止

-   `while (is >> x);`

    一直读取直到末尾

-   `is >> bin;` `is >> oct;` `is >> dec;` `is >> hex;`

    按 2、8、10、16 进制读取数

-   `is >> skipws;`

    忽略前导空格

-   `is.setbase(base);`

    按 `base` 进制读取数 $(2 \le base \le 36)$

-   `is >> reset;`

    取消前面的所有设置

-   `os << x;`

    写入 `x`

-   `os << x << y << z;`

    写入 `x` `y` `z`

-   `os.put(c);`

    写入一个字符 `c`

-   `os.write(x, y, z);`

    写入 `x` `y` `z`

-   `os.flush();` `os << flush;`

    刷新流

-   `os << endl;`

    写入换行

-   `os << ends;`

    写入空格

-   `os << boolalpha;`

    设置写入 `bool` 时用 `true` `false`

-   `os << noboolalpha;`

    设置写入 `bool` 时用 `0` `1`

-   `os << showpos;`

    设置写入正数和 0 时前面加 `+` 号

-   `os << noshowpos;`

    设置写入正数和 0 时前面不加 `+` 号

-   `os << showpoint;`

    设置写入浮点数时严格保留 `setprecision` 时设置的位数

-   `os << noshowpoint;`

    设置写入浮点数时不严格保留 `setprecision` 时设置的位数

-   `os << bin;` `os << oct;` `os << dec;` `os << hex;`

    按 2、8、10、16 进制写入整数

-   `os << lowercase;`

    按大于 10 的进制写入数时，字母大写（默认小写）

-   `os << uppercase;`

    按大于 10 的进制写入数时，字母小写（默认小写）

-   `os << showbase;`

    写入 8、16 进制的数时，在前面显示 `0` `0x`

-   `os << noshowbase;`

    写入 8、16 进制的数时，不在前面显示 `0` `0x`

-   `os << setbase(base);`

    按 `base` 进制写入数，超出范围默认 10 进制 $(2 \le base \le 36)$

-   `os << setw(width);`

    设置下一次写入宽度若小于 `width`，就填补字符（下一次写入重置）

-   `os << setfill(fill);`

    设置 `setw` 填补的字符，默认为空格

-   `os << setprecision(precision);`

    设置浮点数保留位数，默认保留 3 位

-   `os << reset;`

    取消前面的所有设置

-   `ifstream ifs(path);`

    创建文件读流，从 `path` 路径文件读取（也可以是 `FILE*` 文件指针），和普通读流用法相同

-   `ofstream ofs(path);`

    创建文件写流，写入 `path` 路径的文件（也可以是 `FILE*` 文件指针），和普通写流用法相同

# 3. 接口

可以用接口来重载运算符

**注意要用 `fastio::interface::istream` `fastio::interface::ostream` 来重载**

以下是一些示例程序

```cpp
auto &operator<<(fastio::interface::istream &is, string &s) {
    static char buf[1005];
    is >> buf;
    s = buf;
    return is;
}
auto &operator<<(fastio::interface::ostream &os, const string s) { return os << s.c_str(); }
```

```cpp
template<class T> auto& operator<<(fastio::interface::istream& is, const vector<T>& v) {
    v.clear();
    T x;
    int n = is.read<size_t>();
    while (n--) {
        is >> x;
        v.push_back(x);
    }
    return os;
}
template<class T> auto& operator<<(fastio::interface::ostream& os, const vector<T> v) {
    for (T x : v) os << x << ' ';
    return os;
}
```
