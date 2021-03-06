title: Codeforces Beta Round 13 C Sequence
date: 2014-11-21 22:06:59
tags: [ACM, Codeforces, C, DP]
categories: Exercise
toc: true
---
# 题目	
源地址：http://codeforces.com/problemset/problem/13/C

# 理解
给定一个序列，然后对于每一个数，你都可以进行自增或者自减操作。要求求出使得这个序列变为非减序列的最少操作次数。
我一开始的想法比较朴素，我想，只要找到一个比较的标准，比这个标准大我就--，比这个标准小我就++，这样就能得到这个非减序列的最少次操作。然后我就开始寻找这样的标准，后来发现，这是一个不可能的任务。因为给定的序列什么可能都有，我没有办法来衡量每一个数对于整体值的重要程度，然后也没有办法来计算操作的次数。
没有思路之后就开始开脑洞了。很显然，我可以得到这样一个结论，对于一个序列中的某一个数而言，步数最少的，肯定是变成左边或者右边的那个数。如果再考虑到对于整体数列的影响（因为这是一个循环的过程，整个数列都有整体上移或者下移的趋势），这个数可能的取值，肯定是这个数列中已经存在的数。不难猜想，如果这个数变成的最后结果不是这个数列中的数，说明这个解一定不是最优解。（因为要么就多操作了，要么就少操作了。
这么说好像有点难懂，我来举一个栗子吧，就是数列`4 1 9`。很显然，我们一眼就能看出，最优解的状态应该是`4 4 9`，也就是这个1恰好变成了4。试想，如果1变成了3，状态变为` 4 3 9`，不合题意；如果1变成了5，状态变为`4 5 9`，符合题意，但是操作数多了1。那么问题来了，我变成`3 3 9`，难道不好吗？确实是这样，符合题意，而且结果最优。但是我们可以继续想，`3 3 9`可以，`2 2 9`可以吗？再继续，`1 1 9`可以吗？`0 0 9`可以吗？然后我们就能看出，位于`4 4 9`到`1 1 9`之间的数列都是可以的，超过了就不行了。这里的4和1，都是原来数列里面的数。我想，这或许并不是能不能问题，而是算法设计方便的问题。如果取原来数列的数，我们直接进行判断即可；如果不是，我们依然是要取原来数列里的数，判断是否在区间内。
根据上面的讨论，我们不妨得出这样的结论：对任何数进行的操作，最后的结果都是把它们变成原数列中的某个数。
解决了理论上的问题之后，下面进入实际的编码过程。直接开二维数组暴力搞的话，这个问题的时间复杂度过高，不可行。所以我们需要对原数组来一次sort，保证b数组是递增的。然后我们可以看到，dp的过程中，只会用到前后两个数，因此我们可以使用滚动数组来降低空间复杂度。这样，这个问题就得到解了。

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

#define MAXN 5000+10

ll n;
ll a[MAXN];
ll b[MAXN];
ll dp[MAXN];
ll small,ans,flag;

void init()
{
    memset(dp, 0, sizeof(dp));
    scanf("%I64d", &n);
    for(int i=0;i<n;i++)
    {
        scanf("%I64d", &a[i]);
        b[i]=a[i];
    }
    sort(b,b+n);
}

int main(int argc, char const *argv[])
{
    init();
    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
        {
            dp[j]+=abs(a[i]-b[j]);
            if(j>1)
            {
                dp[j]=min(dp[j-1],dp[j]);
            }
        }
    }
    printf("%I64d\n", dp[n-1]);
    return 0;
}
```

# 更新日志
- 2014年11月21日 已AC。