---
title: 单调队列优化dp理解小汇总
date: 2026-3-22 20:29:00
mathjax: true
---

# 回顾单调队列主要思想

单调队列可以维护当前点前面一段区间里的答案来进行转移，通过保持单调性来保留最优且最新的答案，把旧的答案直接跳过。

模板

```cpp
for (int i = 1; i <= n + 1; i++) {
    if (i - Q.front() > k) Q.pop_front();
    dp[i] = dp[Q.front()] + a[i];
    while (!Q.empty() && dp[Q.back()] >= dp[i]) Q.pop_back();
    if (s[i] == '1') {
        Q.clear();
    }
    Q.push_back(i);
    // cout << dp[i] << " ";
}
```
# B.Ropeway
## 观察题目建模
题意解释：可以看作一个数轴上有 $n$ 个点，选取一些点连接，这些点要满足距离不大于 $k$，且这些点将首末相连接，每个点使用的价格不同，接下去有 $q$ 次临时修改一个点的价格，再求其对应的最小价格。

## 观察与单调队列联系
通过朴素的 $dp$ 可以发现得到当前点的答案需要从前面 $k$ 个点转移，因此可以单调队列维护，此时跑一遍后可以得到没有修改过的时候的每个点的答案。然后观察修改这个操作，一个点前后转移顶多只会转移到 $k$ 个以内，因此修改了一个点影响的决策只会包括这个点后面 $k$ 个的决策，$qk$ 的复杂度从题目要求来看也能够接受，因此考虑单点修改了之后对后面 $k$ 个点之外的答案的影响，然后加上后面到当前点的最优后缀的决策，也就是说预处理的时候要处理一个前向的和一个后向的，然后重新处理到 $i$ 这个点的时候加上后缀的答案就行了。

有一点比较重要就是重新处理的时候不能直接开始重新处理，要考虑这个点前面 $k$ 个点的决策，也会对后面的有影响因为可能跳过了这个点，所以要先正常跑前 $k$ 个点跑出单调队列的状态，然后再开始维护新的答案跑后 $k$ 个点。

具体实现：

```cpp
while (q--) {
    int u, v;
    cin >> u >> v;
    if (s[u] == '1') {
        // cout << dp[n + 1] << " " << v << " " << a[u] << endl;
        cout << dp[n + 1] + v - a[u] << endl;
        continue;
    }
    int ans = 1e18;
    // ans = dp[u] + sufdp[u];
    int tmp = a[u];
    a[u] = v;
    Q.clear();
    for (int i = max(0ll, u - k); i <= u - 1; i++) {
        while (!Q.empty() && i - Q.front() > k) Q.pop_front();
        while (!Q.empty() && dp[Q.back()] > dp[i]) Q.pop_back();
        if (s[i] == '1') {
            Q.clear();
        }
        Q.push_back(i);
    }
    for (int i = u; i <= min(n + 1, u + k); i++) {
        while (!Q.empty() && i - Q.front() > k) Q.pop_front();
        dp[i] = dp[Q.front()] + a[i];
        while (!Q.empty() && dp[Q.back()] > dp[i]) Q.pop_back();
        if (s[i] == '1') {
            Q.clear();
        }
        Q.push_back(i);
    }
    for (int i = u; i <= min(n + 1, u + k); i++) {
        ans = min(ans, dp[i] + sufdp[i]);
        // cout << dp[i] << " " << sufdp[i]
        dp[i] = dpre[i];
    }
    a[u] = tmp;
    cout << ans << endl;
}
```