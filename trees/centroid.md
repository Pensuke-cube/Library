# 木の重心・重心分解 / Tree Centroid and Centroid Decomposition

**3/5** · 残る連結成分が全て半分以下になる頂点で木を再帰分割する。O(N log N)。

## 使い方

`centroid_decomposition(g)` に無向木を渡す。`g[v]` は 0 始まりの頂点 `v` に隣接する頂点のリストで、各辺を両方向に登録する。戻り値の `parent[v]` は重心分解で一つ前の段階に選ばれた重心の頂点番号。最初に選ばれた重心は `-1`。この親子は元の木で隣接しているとは限らない。

## コード

```python
def centroid_decomposition(g):
    n = len(g)
    blocked = bytearray(n)
    parent, size, result = [-1]*n, [0]*n, [-1]*n
    tasks = [(0, -1)] if n else []
    while tasks:
        s, cp = tasks.pop()
        order = [s]
        parent[s] = -1
        for v in order:
            size[v] = 1
            for u in g[v]:
                if u != parent[v] and not blocked[u]:
                    parent[u] = v
                    order.append(u)
        for v in reversed(order[1:]):
            size[parent[v]] += size[v]
        half = len(order) // 2
        c = next(v for v in reversed(order) if size[v] > half)
        blocked[c] = 1
        result[c] = cp
        tasks.extend((u, c) for u in g[c] if not blocked[u])
    return result
```

## 考え方

根付き部分木のうち半分を超える最深頂点が重心。頂点対を数えるとき、重心を通る経路を先に処理してから残りの各成分へ進むと、同じ頂点対を重複しない。

### 例題

```python
p = centroid_decomposition([[1], [0,2], [1,3], [2,4], [3]])
assert p[2] == -1 and p.count(-1) == 1
```

[分野の目次](README.md) · [全体の目次](../README.md)
