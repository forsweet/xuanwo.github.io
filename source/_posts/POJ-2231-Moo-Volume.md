title: POJ 2231 Moo Volume
date: 2014-08-16 14:52:02
tags: [ACM, POJ, C, 简单计算, 排序]
categories: Exercise
toc: true
---
# 题目
源地址：http://poj.org/problem?id=2231

# 理解
打表找规律，排序之后发现：
```
1     2     3     4     5  

0     1     2     3     4  
1     0     1     2     3  
2     1     0     1     2  
3     2     1     0     1  
4     3     2     1     0  
```
把下面矩阵的所有数字相加就是所求的结果。

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

int main()
{
    long long int ans = 0, arr[10010];
    int n, m;
    cin >> n;
    for (int i = 0; i < n; ++i)
    {
        cin >> arr[i];
    }
    sort(arr, arr + n);
    for (int i = 0; i < n; ++i)
    {
        ans += (n - 1 - i) * (arr[n - 1 - i] - arr[i]);
    }
    cout << ans * 2 << endl;
    return 0;
}
```

# 更新日志
- 2014年08月16日 已AC。