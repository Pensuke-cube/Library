# 木の直径 / Tree Diameter

**4/5** · 非負重みの木で最も離れた二頂点と距離を O(N) で求める。

## 使い方

`tree_diameter(g)` に空でない無向木を渡す。`g[v]` は 0 始まりの頂点 `v` につながる `(隣接頂点, 非負の重み)` のリスト。各辺は両方向に入れ、重みなしなら 1 を指定する。最も長いパスの `(長さ, 一方の端点, もう一方の端点)` を返す。

## コード

```python
def tree_diameter(g):
    def farthest(s):
        best = (0, s)
        stack = [(s, -1, 0)]
        while stack:
            v, p, d = stack.pop()
            if d > best[0]:
                best = d, v
            for u, w in g[v]:
                if u != p:
                    stack.append((u, v, d+w))
        return best

    _, a = farthest(0)
    d, b = farthest(a)
    return d, a, b
```

## 考え方

任意の頂点から最遠の頂点は直径の端点にできる。そこから最遠点を探し直す。負辺がある最大パスは、子からの寄与の上位二本を集約する木 DP を使う。

### 例題

```python
d, a, b = tree_diameter([[(1, 3)], [(0, 3), (2, 2)], [(1, 2)]])
assert d == 5 and {a,b} == {0,2}
```

[分野の目次](README.md) · [全体の目次](../README.md)
