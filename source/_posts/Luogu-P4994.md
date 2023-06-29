---
title: '[Luogu]P4994'
date: 2020-03-18 10:18:19
tags: '题解'
categories: '递推'
mathjax: true
---
[原题：终于结束的起点](https://www.luogu.com.cn/problem/P4994)
<!--more-->
### 分析

枚举n...判断是否满足$\mathrm{fib}(n) \bmod M = 0, \mathrm{fib}(n + 1) \bmod M = 1$

不过如果直接模拟的话，可能会爆空间

于是进行一个小小的优化：

**迭代！**

我们可以令$f0=0,f1=1;$

然后在递推的时候$f2=(f0+f1) \bmod M;$

然后迭代：$f0=f1,f1=f2;$

就可以极大地节省空间！

### 代码

```cpp
#include<cstdio>
#include<cstring>
#include<iostream>
#include<algorithm>
using namespace std;
long long m;
int main()
{
    cin>>m;
    int f0=0,f1=1;
    for(long long i=1;i<=m*m+1;++i) {
        int f2=(f1+f0)%m;
        if(f2==1 && f1==0) {
            cout<<i;
            return 0;
        }
        f0=f1;f1=f2;
    }
    return 0;
}
```