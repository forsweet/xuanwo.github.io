title: Codeforces Beta Round 7 A Kalevitch and Chess
date: 2014-11-13 19:34:59
tags: [ACM, Codeforces, C, 模拟]
categories: Exercise
toc: true
---
# 题目	
源地址：http://codeforces.com/problemset/problem/7/A

# 理解
同样是理解题- -。
给定一个被黑白棋子占满的棋盘，能进行的操作为将一行或者一列由黑色变白色，问最少需要多少步，能将棋盘全都变为白色。
一开始感觉应该用DFS来做，但是想了想，其实用模拟就能搞定。思路很简单，只要用两层循环，由上到下，由左到右，判断是否为`B`。如果是`B`，则有tmp++；如果不是，则继续。再然后，判断tmp是不是等于8，如果是，则进行一次行的翻转，如果不是，则列的翻转数为tmp。

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

#define MAXN 8

char chess[MAXN][MAXN];
int i,j;
int c=0,r=0;
int tmp=0;
int ans;

void init()
{
    for(int i=0; i<=7; i++)
            scanf("%s", &chess[i]);
}

int main(int argc, char const *argv[])
{
    init();
    for(int i=0; i<=7; i++)
    {
        tmp=0;
        for(j=0; j<=7; j++)
        {
            if(chess[i][j]=='B')
                tmp++;
        }
        if(tmp==MAXN)
        {
            c++;
        }
        else
            r=tmp;
    }
    ans=c+r;
    printf("%d\n", ans);
    return 0;
}
```

# 更新日志
- 2014年11月13日 已AC。