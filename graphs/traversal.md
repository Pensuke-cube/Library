# 幅優先探索・深さ優先探索 / BFS and DFS

**5/5** · 到達可能頂点や辺数距離を O(V+E) で求める。

## 使い方

bfs(g,s) は最短辺数と復元用の親（未到達は -1）。dfs_order(g,s) は到達した頂点。

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
