---
title: 树上背包类DP理解小汇总
date: 2026-3-22 20:29:00
mathjex: true
top_img: transparent
---

# 回顾树上背包主要思想

这里的树上背包主要是模拟对子树的答案合并的过程，也就是类似设 $dp[u][i]$ 在 $u$ 这个点上使用了 $i$ 的资源，然后与 $v$ 的答案通过背包做合并的过程，以下是一个最基础的模板

```cpp
function<void(int, int)> dfs = [&] (int u, int fa) -> void {
    sz[u] = 1;
    for (auto [v, d] : g[u]) {
        if (v == fa) continue;
        dfs(v, u);
        vi tmp(sz[u] + sz[v] + 1);
        for (int i = 0; i <= sz[u] - 1; i++) {
            for (int j = 0; j <= sz[v] - 1; j++) {
                tmp[i + j + 1] = max(tmp[i + j + 1], dp[u][i] + dp[v][j] + d);
            }
        }
        sz[u] += sz[v];
        for (int i = 0; i < sz[u] + sz[v]; i++) {
            dp[u][i] = max(dp[u][i], tmp[i]);
        }
    }
};
```
# I.Infection
## 观察题目建模
由题目可以得知我们最后求的那一片感染的形状是树上的连通块，从一个源点扩展开来，然后题目限制了扩展的数量，因此考虑树上背包点 $u$ 为根的子树下感染了几个点去转移，因为源点只有一个所以考虑把有源点的集合和没有源点的集合合并，没有源点的集合可以和没有源点的集合合并去扩张，且考虑以 $u$ 为根的子树的时候不能感染到上面的节点因此还要乘一个不感染到上一个点的概率。

## 走树上背包流程
当前状态 $dp[i][j][0/1]$ 为以点 $i$ 为根的子树下感染了 $j$ 个点以及下面有没有源点，考虑转移
$$
dp[u][i + j][0] = \sum dp[u][i][0] * dp[v][j][0]
$$
$$
dp[u][i + j][1] = \sum dp[u][i][0] * dp[v][j][1] + dp[u][i][1] * dp[v][j][0]
$$
然后按照模板去写就行了，防止 $dp$ 前后互相影响到可以考虑倒序枚举或者搞一个临时数组更新答案

```cpp
function<void(int, int)> dfs = [&] (int u, int fa) -> void {
    siz[u] = 1;
    dp2[u][1] = a[u] * inv % MOD;
    dp[u][1] = q[u];
    dp[u][0] = (1 - q[u] + MOD) % MOD;
    for (auto v : g[u]) {
        if(v == fa) continue;
        dfs(v, u);
        vi tmp(siz[u] + siz[v] + 1), tmp2(siz[u] + siz[v] + 1);
        for (int i = 1; i <= siz[u]; i++) {
            for (int j = 0; j <= siz[v]; j++) {
                tmp[i + j] = (tmp[i + j] + dp[u][i] * dp[v][j]);
                tmp2[i + j] = (tmp2[i + j] + dp2[u][i] * dp[v][j] + dp[u][i] * dp2[v][j]);
            }
        }
        siz[u] += siz[v];
        for (int i = 1; i <= siz[u]; i++) {
            dp[u][i] = tmp[i];
            dp2[u][i] = tmp2[i];
        }
    }
    for (int i = 1; i <= siz[u]; i++) {
        ans[i] = (ans[i] + dp2[u][i] * (1 - q[fa] + MOD) % MOD) % MOD;
    }
};
```
# A.Alice and Her Lost Cat
## 观察题目建模
这题的建模比较关键，因为单看题面很难理解决策到底是什么样，要解决什么问题，其实本质上是和 Infection 很类似的一道题。题目的约束是叶子的数量，因此记录 $sz$ 的时候其实记录的是这个子树有多少叶子，然后直接根据题目设 $dp$ 的状态会得到 $dp[u][i]$ 表示以 $u$ 为根的子树搜索了 $i$ 个叶子看监控确定猫的位置所需的最小费用，但此时对该干什么仍然一脸懵，这个时候考虑一下看监控这个行为到底干了什么。

考虑一个简单的情况，一个根连了很多点，此时在这个根上看监控，那么下面可以少搜索一个节点，分类讨论一下如果猫在下面能唯一确定，搜不到那就是在没搜的那个，如果猫没经过那看监控可以确定猫不在这里。因此看监控这个行为主要是传递猫在下面的时候能少搜一个点，猫不在的时候能确定这里没有，因此是可以这个子树的叶子少搜一个，也就是说可以让一个叶子不需要被确定，此时就和 Infection 很像了，因此我们就得到的 $dp$ 的完整状态

## 根据状态走流程并设计状态转移方程
$dp[u][i][0/1]$ 表示 $u$ 为根的子树下面搜了 $i$ 个叶子没有/有一个叶子没被确定的情况，然后考虑转移，转移考虑这个点的监控看不看两种情况，不看的话只能让所有节点确定的去转移，或者让有叶子没确定的和全确定的合并，看的话可以让没确定的状态变成确定的状态。

不看监控：
$$
dp[u][i][0] = \min_{\sum j = k}\{ \sum dp[v][j][0]\}
$$
$$
dp[u][i][1] = \min_{\sum j = k \land \sum o = 1}\{\sum dp[v][j][o]\}
$$


看监控：
$$
dp[u][i][0] = a_u + \min_{\sum j = k}\{\sum \min \{ dp[v][j][0], dp[v][j][1]\}\}
$$

根据这个用树上背包转移即可。

```cpp
function<void(int, int)> dfs = [&] (int u, int fa) -> void {
    sz[u] = 0;
    if (g[u].size() == 1 && fa) {
        dp[u][1][0] = a[u];
        dp[u][0][0] = 0;
        dp[u][1][1] = 0;
        sz[u] = 1;
        return;
    }
    dp[u][0][0] = 0, gg[u][0] = 0;
    for (auto v : g[u]) {
        if (v == fa) continue;
        dfs(v, u);
        for (int i = sz[u]; i >= 0; i--) {
            for (int j = sz[v]; j >= 0; j--) {
                dp[u][i + j][0] = min(dp[u][i + j][0], dp[u][i][0] + dp[v][j][0]);
                dp[u][i + j][1] = min({dp[u][i + j][1], dp[u][i][0] + dp[v][j][1], dp[u][i][1] + dp[v][j][0]});
                gg[u][i + j] = min(gg[u][i + j], gg[u][i] + min(dp[v][j][0], dp[v][j][1]));
            }
        }
        sz[u] += sz[v];
    }
    for (int i = 1; i <= sz[u]; i++) {
        dp[u][i][0] = min(dp[u][i][0], gg[u][i] + a[u]);
    }
};
```