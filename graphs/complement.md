# 補グラフ BFS / Complement Graph BFS

**3/5** · 列挙された辺が使えないグラフで、使える辺の最短距離を O(V+E) 期待時間で求める。

## 使い方

`complement_bfs(g, s)` の `g[v]` は頂点 `v` から直接移動できない頂点の集合（`set`）。頂点番号は 0 始まり。無向の場合は禁止辺の両方向を登録する。出発頂点 `s` から、禁止されていない移動だけを使った最短歩数を `d[v]` に返す。`d[s] = 0`、未到達は `-1`。

## コード

```python
from collections import deque

def complement_bfs(g, s):
    remaining = set(range(len(g)))
    remaining.remove(s)
    d = [-1] * len(g)
    d[s] = 0
    q = deque([s])
    while q:
        v = q.popleft()
        keep = g[v]
        reached = remaining - keep
        remaining.intersection_update(keep)
        for u in reached:
            d[u] = d[v] + 1
            q.append(u)
    return d
```

## 考え方

未訪問集合のうち禁止されていない頂点を取り出す。差集合の走査で頂点が残る回は、その分を禁止辺に割り当てられる。距離が確定する頂点は一度だけ消える。

### 例題

```python
assert complement_bfs([{1}, {0,2}, {1}, set()], 0) == [0,2,1,1]
```

[分野の目次](README.md) · [全体の目次](../README.md)
