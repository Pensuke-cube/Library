# 最小全域木・クラスカル法 / Minimum Spanning Tree / Kruskal

**4/5** · 全頂点をつなぐ最小費用の森を O(E log E+V) で求める。

## 使い方

[Union-Find](../structures/dsu.md)を先に置く。kruskal(n,edges) の辺は (u,v,w)。合計重みと採用辺を返す。

## コード

```python
def kruskal(n, edges):
    d = DSU(n)
    total = 0
    chosen = []
    for u, v, w in sorted(edges, key=lambda e: e[2]):
        if d.merge(u, v):
            total += w
            chosen.append((u, v, w))
            if len(chosen) == n - 1:
                break
    return total, chosen
```

## 考え方

辺を安い順に見て閉路を作らないものを加える。この辺で分かれていた成分を結ぶ他の候補は同額以上。採用辺が V-1 未満なら非連結。

### 例題

```python
w, chosen = kruskal(3, [(0,1,4), (0,2,2), (1,2,1)])
assert w == 3 and len(chosen) == 2
```

[分野の目次](README.md) · [全体の目次](../README.md)
