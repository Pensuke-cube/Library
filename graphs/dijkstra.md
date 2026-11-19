# ダイクストラ法 / Dijkstra's Algorithm

**5/5** · 非負重みグラフの単一始点最短距離を O(V+E log(E+1)) で求める。

## 使い方

`dijkstra(g, s)` の `g[v]` は `v` から出る辺 `(行き先, 重み)` のリスト。頂点番号は 0 始まりで、重みは非負。無向辺は両方向を入れる。`s` に出発頂点を渡す。

- `d[v]` は `s` から `v` への最短距離。未到達は `float("inf")`。
- `parent[v]` は最短経路上で `v` の直前の頂点。`s` 自身と未到達頂点では `-1`。戻り値は `(d, parent)`。

## コード

```python
from heapq import heappop, heappush

def dijkstra(g, s):
    d = [float("inf")] * len(g)
    p = [-1] * len(g)
    d[s] = 0
    heap = [(0, s)]
    while heap:
        dv, v = heappop(heap)
        if dv != d[v]:
            continue
        for u, w in g[v]:
            nd = dv + w
            if nd < d[u]:
                d[u] = nd
                p[u] = v
                heappush(heap, (nd, u))
    return d, p
```

## 考え方

候補の最小距離をヒープで取り出す。重みが非負なら、未確定の頂点を経由してこの距離を下げることはできない。最短経路数を数える典型実装は正重みで使う。

### 例題

```python
d, p = dijkstra([[(1, 5), (2, 1)], [], [(1, 2)]], 0)
assert d == [0, 3, 1] and p[1] == 2
```

[分野の目次](README.md) · [全体の目次](../README.md)
