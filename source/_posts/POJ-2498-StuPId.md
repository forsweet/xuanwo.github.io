title: POJ 2498 StuPId
date: 2014-08-16 16:12:54
tags: [ACM, POJ, C, 简单计算]
categories: Exercise
toc: true
---
# 题目
源地址：http://poj.org/problem?id=2498

# 理解
英文题= =。按照{9,3,7}的顺序，从后往前乘，最后的乘积相加可以被十整除。但是有一个数字看不清了，要求计算出那个数字，并且输出整个数。

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
#define debug puts("-----")
#define pi (acos(-1.0))
#define eps (1e-8)
#define inf (1<<30)
using namespace std;

int main(int argc, char const *argv[])
{
    int t, testCase, i, v[3] = {9, 3, 7};
    char num[10];
    scanf("%d", &testCase);
    for (t = 1; t <= testCase; t ++)
    {
        scanf("%s", num);
        int sum = 0, p = 0, w, k;
        for (i = strlen(num) - 1; i >= 0; i --)
        {
            if (num[i] == '?')
            {
                w = v[p];
                k = i;
            }
            else sum += (num[i] - '0') * v[p];
            p ++;
            if (p == 3) p = 0;
        }
        for (i = 0; i < 10; i ++)
            if ((sum + i * w) % 10 == 0)
            {
                num[k] = '0' + i;
                printf("Scenario #%d:\n%s\n\n", t, num);
                break;
            }
    }
    return 0;
}
```

# 更新日志
- 2014年08月16日 已AC。