# グリッド DP / Grid DP

**5/5** · 右・下に進む経路数を O(HW) 時間・O(W) 空間で求める。

## 使い方

grid_paths(grid,mod) は左上から右下までの経路数。壁は "#"。空でない長方形を渡す。

## コード

```python
def grid_paths(grid, mod):
    dp = [0] * len(grid[0])
    dp[0] = 1
    for row in grid:
        for j, c in enumerate(row):
            if c == "#":
                dp[j] = 0
            elif j:
                dp[j] = (dp[j] + dp[j-1]) % mod
    return dp[-1] % mod
```

## 考え方

上と左からの経路を足す。有効な遷移が一方向なら位置に順序を付けられる。四方向で巡回可能な最短距離では BFS などを使う。

### 例題

```python
assert grid_paths(["...", ".#.", "..."], 998244353) == 2
```

[分野の目次](README.md) · [全体の目次](../README.md)
