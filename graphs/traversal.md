# 幅優先探索・深さ優先探索 / BFS and DFS

**5/5** · 到達可能頂点や辺数距離を O(V+E) で求める。

## 使い方

`g[v]` に頂点 `v` から直接行ける頂点番号を並べる。頂点番号は 0 始まり。無向辺は両方向を入れる。`s` は出発頂点。

- `bfs(g, s)` は `(dist, parent)`。`dist[v]` は最短で通る辺数で、未到達なら `-1`。`parent[v]` はその経路の一つで `v` の直前の頂点。出発点と未到達頂点の親は `-1`。
- `dfs_order(g, s)` は `s` から到達した頂点を、スタックから取り出した順に返す。

## コード

```python
from collections import deque

def bfs(g, s):
    dist = [-1] * len(g)
    parent = [-1] * len(g)
    dist[s] = 0
    q = deque([s])
    while q:
        v = q.popleft()
        for u in g[v]:
            if dist[u] == -1:
                dist[u] = dist[v] + 1
                parent[u] = v
                q.append(u)
    return dist, parent

def dfs_order(g, s):
    seen = bytearray(len(g))
    seen[s] = 1
    stack = [s]
    order = []
    while stack:
        v = stack.pop()
        order.append(v)
        for u in reversed(g[v]):
            if not seen[u]:
                seen[u] = 1
                stack.append(u)
    return order
```

## 考え方

BFS は近い順に確定する。親を到達点から辿って逆順にすると最短経路になる。DFS で厳密な再帰の訪問順・退出順が必要なら、スタックに各頂点の次に調べる辺も記録する。

### 例題

```python
g = [[1, 2], [3], [3], []]
d, p = bfs(g, 0)
assert d == [0, 1, 1, 2] and p[3] == 1
assert set(dfs_order(g, 0)) == {0, 1, 2, 3}
```

[分野の目次](README.md) · [全体の目次](../README.md)
