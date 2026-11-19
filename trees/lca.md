# 最小共通祖先・木の距離 / Lowest Common Ancestor

**4/5** · 前処理 O(N log N)、LCA・距離を O(log N) で求める。

## 使い方

[根付き化](euler-tour.md)のコードを先に置く。`LCA(g, root=0)` の `g[v]` に頂点 `v` の隣接先を並べる。空でない無向木を使い、頂点番号は 0 始まり、辺は両方向を登録する。`root` は根にする頂点番号。

`lca(u, v)` は `u` と `v` の共通祖先のうち根から最も深い頂点番号（自身も祖先に含む）。`distance(u, v)` は二頂点間のパスの辺数。

## コード

```python
class LCA:
    def __init__(self, g, root=0):
        parent, self.depth, _, _, _ = root_tree(g, root)
        parent[root] = root
        self.up = [parent]
        for _ in range(1, len(g).bit_length()):
            p = self.up[-1]
            self.up.append([p[x] for x in p])

    def lca(self, u, v):
        d = self.depth
        if d[u] < d[v]:
            u, v = v, u
        diff = d[u] - d[v]
        for k in range(diff.bit_length()):
            if diff >> k & 1:
                u = self.up[k][u]
        if u == v:
            return u
        for p in reversed(self.up):
            if p[u] != p[v]:
                u, v = p[u], p[v]
        return self.up[0][u]

    def distance(self, u, v):
        d = self.depth
        return d[u] + d[v] - 2 * d[self.lca(u, v)]
```

## 考え方

先に深さを揃え、共通祖先を越えない最大の跳躍を繰り返す。距離は両頂点から共通祖先までの距離の和。重み付きでは根からの距離を別に記録する。

### 例題

```python
lca = LCA([[1,2], [0,3,4], [0], [1], [1]])
assert lca.lca(3,4) == 1 and lca.distance(2,4) == 3
```

[分野の目次](README.md) · [全体の目次](../README.md)
