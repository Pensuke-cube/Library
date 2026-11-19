# ナップサック DP / Knapsack DP

**5/5** · 各品物を高々一度選んで容量 W 以下で価値を最大化する。O(NW)。

## 使い方

`knapsack(items, capacity)` に品物の列 `items` と容量 `capacity`（0 以上の整数）を渡す。各品物は `(重さ, 価値)` の組で、重さは 0 以上の整数。各品物を高々一度選び、合計重量が容量以下になる価値の最大和を返す。何も選ばない場合も含む。

## コード

```python
def knapsack(items, capacity):
    dp = [0] * (capacity + 1)
    for w, v in items:
        for c in range(capacity, w-1, -1):
            candidate = dp[c-w] + v
            if candidate > dp[c]:
                dp[c] = candidate
    return dp[capacity]
```

## 考え方

降順更新なら同じ品物の更新前の値を参照する。重さが正で何度でも取れる場合は昇順。容量が大きく価値の総和が小さいなら、価値ごとに必要な最小重量を持つ。

### 例題

```python
assert knapsack([(2,3),(1,2),(3,4)], 4) == 6
```

[分野の目次](README.md) · [全体の目次](../README.md)
