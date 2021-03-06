title: Codeforces Beta Round 15 C Industrial Nim
date: 2014-11-26 14:25:00
tags: [ACM, Codeforces, C, 博弈]
categories: Exercise
toc: true
---
# 题目	
源地址：http://codeforces.com/problemset/problem/15/C

# 理解
有n个矿场，第i个矿场有mi辆矿车，第一辆矿车有xi颗石头，第二辆xi+1颗，如此递推，直到第mi辆有mi+xi-1颗。然后有两个人轮流取石头（金矿？），他们可以选择任意一个矿场任意一辆矿车取走任意非0数量的石头，直到第一个不能再取的人认输。
实际上，这就是一个裸的Nim博弈问题，只要直接运用结论就能完成解答。但是问题在于，数据太多，导致每一个全都异或起来的话耗时太长。所以需要采用一些手段处理一下。我们需要用到两个结论：第一，从1异或到n的答案存在着这样一个特性：n%4==1时，答案为1；n%4==2时，答案为x+1；n%4==3时，答案为0；n%4==4时，答案为x。第二，从x异或到y的值等于nim(x-1)^nim(y)。
经过上述的处理，最后的结果就出来了~

<!-- more -->

# 代码
```
#include <cstdio>
#include <cstdlib>
#include <cstring>
#include <cmath>
#include <ctime>
#include <iostream>
#include <algorithm>
#include <string>
#include <vector>
#include <deque>
#include <list>
#include <set>
#include <map>
#include <stack>
#include <queue>
#include <numeric>
#include <iomanip>
#include <bitset>
#include <sstream>
#include <fstream>
#define debug "output for debug\n"
#define pi (acos(-1.0))
#define eps (1e-8)
#define inf 0x3f3f3f3f
#define ll long long int
using namespace std;

#define MAXN 100000+10

ll n,x,m,ans=0;

ll nim(ll x)
{
    ll tmp=x%4;
    if(tmp==1)
        return 1;
    else if(tmp==2)
        return x+1;
    else if(tmp==3)
        return 0;
    else
        return x;
}

int main(int argc, char const *argv[])
{
    scanf("%I64d", &n);
    while(n--)
    {
        scanf("%I64d %I64d", &x, &m);
        m=nim(m+x-1);
        x=nim(x-1);
        ans^=x^m;
    }
    ans?puts("tolik"):puts("bolik");
    return 0;
}
```

# 更新日志
- 2014年11月26日 已AC。