# ベルマン–フォード法 / Bellman–Ford Algorithm

**4/5** · 負辺を含む最短距離と負閉路の影響範囲を O(VE+V) で求める。

## 使い方

bellman_ford(n,edges,s) の辺は (始点,終点,重み)。未到達は inf、負閉路の影響を受ける頂点は -inf。

## コード

```python
from collections import deque

def bellman_ford(n, edges, s):
    edges = list(edges)
    inf = float("inf")
    d = [inf] * n
    d[s] = 0
    for _ in range(n - 1):
        changed = False
        for u, v, w in edges:
            if d[u] == inf:
                continue
            nd = d[u] + w
            if nd < d[v]:
                d[v] = nd
                changed = True
        if not changed:
            return d
    g = [[] for _ in range(n)]
    q = deque()
    for u, v, w in edges:
        g[u].append(v)
        if d[u] != inf and d[u] + w < d[v]:
            d[v] = -inf
            q.append(v)
    while q:
        for v in g[q.popleft()]:
            if d[v] != -inf:
                d[v] = -inf
                q.append(v)
    return d
```

## 考え方

単純路は高々 V-1 辺なので、それを超えて改善できるなら到達可能な負閉路がある。改善した頂点から到達できる先も距離を任意に下げられる。

### 例題

```python
assert bellman_ford(4, [(0,1,1),(1,2,-2),(2,1,0),(2,3,5)], 0) == [0, -float("inf"), -float("inf"), -float("inf")]
```

[分野の目次](README.md) · [全体の目次](../README.md)
