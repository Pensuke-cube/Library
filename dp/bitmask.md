# ビット DP・巡回セールスマン / Bitmask DP / Traveling Salesman

**4/5** · 訪問集合を状態にして巡回路の最小費用を O(N²2^N) で求める。

## 使い方

tsp(cost) は頂点 0 を出発して全頂点を訪れ 0 に戻る最小費用。辺なしは inf。

## コード

```python
def tsp(cost):
    n = len(cost)
    if n <= 1:
        return 0
    full = (1 << n) - 1
    inf = float("inf")
    dp = [[inf] * n for _ in range(full + 1)]
    dp[1][0] = 0
    for mask in range(1, full, 2):
        for v, value in enumerate(dp[mask]):
            if value == inf:
                continue
            remaining = full ^ mask
            while remaining:
                bit = remaining & -remaining
                remaining ^= bit
                u = bit.bit_length() - 1
                row = dp[mask | bit]
                row[u] = min(row[u], value + cost[v][u])
    return min(dp[full][v]+cost[v][0] for v in range(1,n))
```

## 考え方

状態は訪問済み集合と末尾の頂点。同じ状態から先の選択肢は訪問順に依存しないので最安値だけ残す。二部割当の数え上げなら mask のビット数が左側の処理数になる。

### 例題

```python
assert tsp([[0,2,6],[2,0,3],[6,3,0]]) == 11
```

[分野の目次](README.md) · [全体の目次](../README.md)
