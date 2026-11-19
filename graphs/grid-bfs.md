# グリッド探索 / Grid BFS

**5/5** · 壁のある H×W マスで上下左右の最短歩数を O(HW) で求める。

## 使い方

`grid_bfs(grid, sr, sc)` に空でない長方形の文字グリッドを渡す。`grid[r][c]` は行 `r`・列 `c` の文字で、`"#"` は壁。`(sr, sc)` は 0 始まりの通行可能な出発マス。上下左右への移動だけを使った最短歩数を `d[r][c]` に返し、壁や未到達マスは `-1`。

## コード

```python
from collections import deque

def grid_bfs(grid, sr, sc):
    h, w = len(grid), len(grid[0])
    d = [[-1] * w for _ in range(h)]
    d[sr][sc] = 0
    q = deque([(sr, sc)])
    while q:
        r, c = q.popleft()
        nd = d[r][c] + 1
        for nr, nc in ((r-1,c), (r+1,c), (r,c-1), (r,c+1)):
            if 0 <= nr < h and 0 <= nc < w and grid[nr][nc] != "#" and d[nr][nc] < 0:
                d[nr][nc] = nd
                q.append((nr, nc))
    return d
```

## 考え方

マスを頂点、隣接移動を辺にする。複数の始点から一番近い距離が欲しければ、全始点を距離 0 でキューに入れる。向きや鍵を持つ場合はそれも頂点の状態に含める。

### 例題

```python
assert grid_bfs([".#.", "..."], 0, 0)[0][2] == 4
```

[分野の目次](README.md) · [全体の目次](../README.md)
