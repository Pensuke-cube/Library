# 重軽分解 / Heavy-Light Decomposition

**3/5** · 木のパスを O(log N) 個の連続区間に分解する。構築 O(N)。

## 使い方

HLD(g,root) の path(u,v) は両端を含む頂点パスを半開区間 (l,r) に分解。順序を問わない演算用。各頂点の位置は pos[v]。

## コード

```python
class HLD:
    def __init__(self, g, root=0):
        n = len(g)
        p, d = [-1]*n, [0]*n
        order = [root]
        for v in order:
            for u in g[v]:
                if u != p[v]:
                    p[u], d[u] = v, d[v]+1
                    order.append(u)
        size, heavy = [1]*n, [-1]*n
        for v in reversed(order[1:]):
            a = p[v]
            size[a] += size[v]
            if heavy[a] < 0 or size[v] > size[heavy[a]]:
                heavy[a] = v
        head, pos = [0]*n, [0]*n
        starts = [root]
        i = 0
        while starts:
            v = h = starts.pop()
            while v >= 0:
                head[v], pos[v] = h, i
                i += 1
                starts.extend(u for u in g[v] if u != p[v] and u != heavy[v])
                v = heavy[v]
        self.parent, self.depth, self.head, self.pos = p, d, head, pos
        self.size = size

    def path(self, a, b):
        p, d, head, pos = self.parent, self.depth, self.head, self.pos
        while head[a] != head[b]:
            if d[head[a]] < d[head[b]]:
                a, b = b, a
            h = head[a]
            yield pos[h], pos[a]+1
            a = p[h]
        yield min(pos[a], pos[b]), max(pos[a], pos[b])+1
```

## 考え方

各頂点で最大の子への辺を重辺にする。それ以外の辺を下ると部分木サイズが半分以下になり、パス上に高々 O(log N) 本。セグメント木と組み合わせれば区間集約は O(log² N)。部分木は [pos[v],pos[v]+size[v])。

### 例題

```python
h = HLD([[1,2], [0,3,4], [0], [1], [1]])
positions = {x for l,r in h.path(2,4) for x in range(l,r)}
assert positions == {h.pos[v] for v in [2,0,1,4]}
```

[分野の目次](README.md) · [全体の目次](../README.md)
