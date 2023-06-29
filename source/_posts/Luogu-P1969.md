---
title: '[Luogu]P1969'
date: 2020-03-18 10:17:18
tags: '题解'
categories: '贪心'
---
[原题：积木大赛](https://www.luogu.com.cn/problem/P1969)
<!--more-->
### 分析

比较简单的**贪心**

考虑最优的**建造策略**：

每次选择最左边的一个还未建好的积木，将其高度加一，同时使右边尽可能多的积木高度也加一（注意要是**连续**的一段）。

简单地证明一下：对于一个未建好的积木，如果不在当前这一步将其高度加一，则必然要在后面的某一步中加上，在当前加上至少不会更差。

**计算方案**：

直接模拟会TLE...

所以稍加思索就会发现：

我们可以考虑**每一个积木作为最左边的时候高度加一的次数**；

当该积木比上一个矮时显然次数为0；

当该积木比上一个高时，还需要的次数即为该积木的高度减去上一个的高度。

### 代码

```cpp
#include<iostream>
#include<cstdio>
#include<cstring>
using namespace std;
const int maxn=100000+10;
int n;
int h[maxn],p[maxn];

int read(int &x) {
    int f=1;
    x=0;
    char c=getchar();
    while(c>'9' || c<'0') {
        if(c=='-') f=-1;
        c=getchar();
    }
    while(c>='0' && c<='9') {
        x=x*10+c-'0';
        c=getchar();
    }
    return x*f;
}

int main() {
    read(n);
    for(int i=1; i<=n; ++i) read(h[i]);
    h[0]=0;
    int ans=0;
    for(int i=1; i<=n; ++i) {
        if(h[i]>h[i-1]) ans+=h[i]-h[i-1];
    }
    printf("%d",ans);
    return 0;
}
```