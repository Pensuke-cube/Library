# 確率・期待値 DP / Probability and Expectation DP

**4/5** · 状態ごとの確率や期待値を遷移式で集約する。例は O(N²)。

## 使い方

`heads_distribution(p)` に独立なコインの表が出る確率を順に渡す。各値は 0 以上 1 以下（例 `0.5`）。結果の `dp[k]` はちょうど `k` 枚が表になる確率で、長さはコインの枚数 + 1。

## コード

```python
def heads_distribution(p):
    dp = [1.0]
    for x in p:
        dp.append(0.0)
        for k in range(len(dp)-1, 0, -1):
            dp[k] = dp[k]*(1-x) + dp[k-1]*x
        dp[0] *= 1-x
    return dp
```

## 考え方

確率は分岐先に確率を掛けて足す。期待値は「今回の費用＋次の期待値の加重和」。確率 p で同じ状態に戻るなら右辺の pE を左へ移し、残りを 1-p で割る。

### 例題

```python
p = heads_distribution([0.5, 0.5])
assert p == [0.25, 0.5, 0.25]
```

[分野の目次](README.md) · [全体の目次](../README.md)
