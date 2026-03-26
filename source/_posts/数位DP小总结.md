---
title: 数位dp小总结
date: 2026-3-22 20:29:00
mathjex: true
top_img: transparent
---

# 回顾数位DP主要思想

数位DP是从按照题目要求匹配数字位，按照我的理解每位的状态分为2种（大部分情况下）：  
1. 从前面（高位）到现在为止都完全匹配，此时还需要根据约束去走  
2. 从前面（高位）到现在有一位解放了约束可以随便放  
然后按照这个流程去算方案数

# M.Xor Sum
广州2022CCPC
## 由异或求和想到拆位

异或求和位与位之间是没有联系的，因此只需要考虑一位上的01数量，设有$k$个数，在$p$位有$cnt_1$个1，$k-cnt_1$个0，此时这一位贡献为$(k-cnt_1)*cnt_1 \times 2^{p}$，此时这一位的方案数是$\binom{k}{cnt_1}$。

## 走数位DP流程

因为贡献的前面有一个组合数的系数，会比较大，观察数据范围也会发现$n$比$m$大很多，所以这一位做了操作是可以影响答案上当前位前面的更高位需求的，因此可以统计当前这一位答案目前需求的数量，同时$a_i$的大小是由$m$进行约束的，因此考虑从高位到低位走去满足约束，记录满足约束上界当前这一位数字不能乱放的数的数量（如果$a_i$的高位部分与$m$一一对应，那么当前位如果$m$上是0那这个$a_i$是不能放1的）。

因此就可以得到递归需要的数据是: $p$当前位，$lima$不能随便放1的$a_i$的数量，$need$当前的需求。

考虑边界条件：$need>=0$

此时DP所需的所有东西就都齐了，记得记忆化搜索就行
$$
dp[q][now][x] += dfs(q - 1, i, need \times 2 + \text{(n >> dep \& 1)} - (i + j) \times (k - i - j))
$$
这是m当前位上为1的情况,为0的时候不需要考虑那些吃满前面上限的数字的情况。

```cpp
int dfs (int dep, int p, int x) {
    if (dep < 0) {
        if (x == 0) return 1;
        else return 0;
    }
    if (x < 0 || x > (k - k / 2) * (k / 2)) return 0;
    if (dp[dep][p][x] != -1) return dp[dep][p][x];
    dp[dep][p][x] = 0;
    int add = n >> dep & 1;
    if (m >> dep & 1) {
        for (int i = 0; i <= p; i++) {
            for (int j = 0; j + i <= k; j++) {
                (dp[dep][p][x] += dfs(dep - 1, i, x * 2 - (i + j) * (k - i - j) + 
                add) * C[p][i] % MOD * C[k - p][j] % MOD) %= MOD;
            }
        }
    } else {
        for (int i = 0; i <= k - p; i++) {
            (dp[dep][p][x] += dfs(dep - 1, p, x * 2 - i * (k - i) + add) * C[k - p]
            [i] % MOD) %= MOD;
        }
    }
    return dp[dep][p][x];
}
```