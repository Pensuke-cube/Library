# 単調性を使う DP 最適化 / Dynamic Programming Optimization

**3/5** · 単調な最良分割点を使い、一行の分割 DP を O(N log N) で更新する。

## 使い方

`monotone_dp_row(prev, cost)` の `prev[j]` に一つ前の DP 行（添字 `0` から `N`）、`cost(j, i)` に分割点 `j` から `i` への費用を返す関数を渡す。結果の `dp[i]` は `0 <= j < i` での `prev[j] + cost(j, i)` の最小値。`dp[0]` は `float("inf")`。同点なら最小の `j` を選んだとき、その `j` が `i` とともに非減少であること。

## コード

```python
def monotone_dp_row(prev, cost):
    n = len(prev)-1
    inf = float("inf")
    dp = [inf] * (n+1)
    tasks = [(1,n,0,n-1)]
    while tasks:
        l, r, low, high = tasks.pop()
        if l > r:
            continue
        i = (l+r)//2
        best = low
        for j in range(low,min(high,i-1)+1):
            value = prev[j]+cost(j,i)
            if value < dp[i]:
                dp[i], best = value, j
        tasks.append((l,i-1,low,best))
        tasks.append((i+1,r,best,high))
    return dp
```

## 考え方

中央を先に解き、その最良分割点で左右の探索範囲を切る。同値なら小さい分割点を選ぶ。適用前に Monge 性などから単調性を示す。コストが直線の最小値に変形できる場合は凸包最適化や Li Chao 木も候補。

### 例題

```python
prev = [0,1,4,9,16,25]
dp = monotone_dp_row(prev, lambda l,r: (r-l)**2)
assert dp[1:] == [1,2,5,8,13]
```

[分野の目次](README.md) · [全体の目次](../README.md)
