# 強連結成分分解 / Strongly Connected Components

**4/5** · 互いに行き来できる頂点を O(V+E) でグループ化する。

## 使い方

scc(g) は (頂点ごとの成分番号, 成分の頂点列)。異なる成分間の辺は番号が小さい方から大きい方へ向かう。

## コード

```python
def scc(g):
    n = len(g)
    rg = [[] for _ in range(n)]
    for v, row in enumerate(g):
        for u in row:
            rg[u].append(v)
    seen = bytearray(n)
    order = []
    for s in range(n):
        if seen[s]:
            continue
        stack = [s]
        while stack:
            v = stack.pop()
            if v < 0:
                order.append(~v)
            elif not seen[v]:
                seen[v] = 1
                stack.append(~v)
                stack.extend(u for u in g[v] if not seen[u])
    ids = [-1] * n
    groups = []
    for s in reversed(order):
        if ids[s] >= 0:
            continue
        k = len(groups)
        ids[s] = k
        group = []
        stack = [s]
        while stack:
            v = stack.pop()
            group.append(v)
            for u in rg[v]:
                if ids[u] < 0:
                    ids[u] = k
                    stack.append(u)
        groups.append(group)
    return ids, groups
```

## 考え方

元のグラフで DFS の退出順を記録する。退出順を逆から見て逆辺を辿ると、成分を一つずつ取れる。各成分を縮約すると DAG になる。

### 例題

```python
ids, groups = scc([[1], [0, 2], [3], [2]])
assert ids == [0, 0, 1, 1] and len(groups) == 2
```

[分野の目次](README.md) · [全体の目次](../README.md)
