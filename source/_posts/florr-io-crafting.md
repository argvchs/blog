---
title: 计算 Florr.io 合卡概率
date: 2023-06-10 05:43:08
tags:
    - Florr.io
categories: 算法
---

写了一个 [Florr.io](https://florr.io) 合卡概率计算器

<!-- more -->

设 $a_n$ 表示消耗 $n$ 个卡期望合成卡的数量，若合成概率为 $p$，则

$$
a_n =
\begin{cases}
0, & n < 5 \\
p\left(a_{n - 5} + 1\right) + \left(1 - p\right)\left(\frac{1}{4}a_{n - 4} + \frac{1}{4}a_{n - 3} + \frac{1}{4}a_{n - 2} + \frac{1}{4}a_{n - 1}\right), & n \geq 5 \\
\end{cases}
$$

转换为矩阵乘法即为

$$
\begin{bmatrix}
a_n \\
a_{n + 1} \\
a_{n + 2} \\
a_{n + 3} \\
a_{n + 4} \\
p
\end{bmatrix}
=
\begin{bmatrix}
0 & 1 & 0 & 0 & 0 & 0 \\
0 & 0 & 1 & 0 & 0 & 0 \\
0 & 0 & 0 & 1 & 0 & 0 \\
0 & 0 & 0 & 0 & 1 & 0 \\
p & q & q & q & q & 1 \\
0 & 0 & 0 & 0 & 0 & 1
\end{bmatrix}
^ n
\begin{bmatrix}
a_0 \\
a_1 \\
a_2 \\
a_3 \\
a_4 \\
p
\end{bmatrix}
$$

其中 $q = \dfrac{1 - p}{4}$

```cpp
#include <iomanip>
#include <iostream>
using namespace std;
typedef double matrix[15][15];
long long n;
double p, q;
matrix a, b;
void zero(matrix a) {
    for (int i = 1; i <= 10; i++)
        for (int j = 1; j <= 10; j++) a[i][j] = 0;
}
void unit(matrix a) {
    for (int i = 1; i <= 10; i++)
        for (int j = 1; j <= 10; j++) a[i][j] = i == j;
}
// a = b
void assign(matrix a, matrix b) {
    for (int i = 1; i <= 10; i++)
        for (int j = 1; j <= 10; j++) a[i][j] = b[i][j];
}
void assign(matrix a, initializer_list<initializer_list<double>> b) {
    for (int i = 1; i <= (int)b.size(); i++)
        for (int j = 1; j <= (int)b.begin()[i - 1].size(); j++)
            a[i][j] = b.begin()[i - 1].begin()[j - 1];
}
// a = b * c
void product(matrix a, matrix b, matrix c) {
    matrix a0;
    zero(a0);
    for (int i = 1; i <= 10; i++)
        for (int j = 1; j <= 10; j++)
            for (int k = 1; k <= 10; k++) a0[i][j] += b[i][k] * c[k][j];
    assign(a, a0);
}
// a = b ^ n
void power(matrix a, matrix b, long long n) {
    matrix a0, b0;
    unit(a0);
    assign(b0, b);
    while (n) {
        if (n & 1) product(a0, a0, b0);
        product(b0, b0, b0);
        n >>= 1;
    }
    assign(a, a0);
}
int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    cin >> n >> p;
    q = (1 - p) / 4;
    assign(a, {{0}, {0}, {0}, {0}, {0}, {p}});
    assign(b, {
                  {0, 1, 0, 0, 0, 0},
                  {0, 0, 1, 0, 0, 0},
                  {0, 0, 0, 1, 0, 0},
                  {0, 0, 0, 0, 1, 0},
                  {p, q, q, q, q, 1},
                  {0, 0, 0, 0, 0, 1},
              });
    power(b, b, n);
    product(a, b, a);
    cout << fixed << setprecision(3) << a[1][1];
    return 0;
}
```