# 0-1 BFS / 0-1 Breadth-First Search

**4/5** · 重みが 0 または 1 のグラフの最短距離を O(V+E) で求める。

## 使い方

bfs01(g,s)。g[v] の各要素は (行き先,重み)。未到達は inf。

## コード

```python
from collections import deque

def bfs01(g, s):
    d = [float("inf")] * len(g)
    d[s] = 0
    q = deque([(0, s)])
    while q:
        dv, v = q.popleft()
        if dv != d[v]:
            continue
        for u, w in g[v]:
            nd = dv + w
            if nd < d[u]:
                d[u] = nd
                if w:
                    q.append((nd, u))
                else:
                    q.appendleft((nd, u))
    return d
```

## 考え方

重み 0 の候補は現在と同じ距離なので先頭へ、重み 1 は末尾へ入れる。既に改善された古い候補は読み飛ばす。

### 例題

```python
assert bfs01([[(1, 1), (2, 0)], [], [(1, 0)]], 0) == [0, 0, 0]
```

[分野の目次](README.md) · [全体の目次](../README.md)
