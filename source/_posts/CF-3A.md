title: Codeforces Beta Round 3 A Shortest path of the king
date: 2014-11-3 11:03:26
tags: [ACM, Codeforces, C, 模拟]
categories: Exercise
toc: true
---
# 题目	
源地址：http://codeforces.com/contest/3/problem/A

# 理解
第一开始的想法是可以用DFS或者BFS搞定。后来仔细想了想，发现其实不需要这么复杂，通过建立一个坐标系，可以轻松搞定这个问题。
首先坐标化，将A~H转化为1~8，方便后续的处理，同时计算出终点与起点位移在x，y轴上的投影，分别设为mx，my。
然后下面是模拟的步骤：
- 处理斜角：循环对mx和my进行递增或者递减的操作，直到有一个值变为零。
- 处理直线：对mx或者my进行递增或者递减的操作，直到这个值也为零，此时已经模拟完毕。

有两个值得注意的地方：
- 首先需要输出步数，很显然，步数就是`max(abs(mx),abs(my))`。
- 不需要记忆路径，每次处理mx和my的时候，顺便把路径输出即可。

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

char a[10];
int sx,sy,ex,ey;
int ans;
int mx,my;

void init()
{
    gets(a);
    sx=a[0]-'a'+1;
    sy=a[1]-'0';
    gets(a);
    ex=a[0]-'a'+1;
    ey=a[1]-'0';
    mx=ex-sx;
    my=ey-sy;
}

int main(int argc, char const *argv[])
{
    init();
    ans=max(abs(mx),abs(my));
    printf("%d\n", ans);
    while(mx*my!=0)
    {
        if(mx>0&&my>0)
        {
            printf("RU\n");
            mx--;
            my--;
        }
        else if(mx>0&&my<0)
        {
            printf("RD\n");
            mx--;
            my++;
        }
        else if(mx<0&&my>0)
        {
            printf("LU\n");
            mx++;
            my--;
        }
        else
        {
            printf("LD\n");
            mx++;
            my++;
        }
    }
    if(mx>0)
    {
        while(mx>0)
        {
            printf("R\n");
            mx--;
        }
    }
    else if(mx<0)
    {
        while(mx<0)
        {
            printf("L\n");
            mx++;
        }
    }
    else if(my>0)
    {
        while(my>0)
        {
            printf("U\n");
            my--;
        }
    }
    else
    {
        while(my<0)
        {
            printf("D\n");
            my++;
        }
    }
	return 0;
}
```

# 更新日志
- 2014年11月3日 已AC。