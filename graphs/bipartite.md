# 二部グラフ判定 / Bipartite Graph Test

**4/5** · 無向グラフを隣同士で色が違う二色に塗れるか O(V+E) で判定する。

## 使い方

`bipartite(g)` の `g[v]` に頂点 `v` の隣接先を並べる。頂点番号は 0 始まりで、無向辺の両方向を登録する。隣り合う頂点を異なる色にできれば `color[v]` が `0` または `1` のリストを返す。できなければ `None`。

## コード

```python
def bipartite(g):
    color = [-1] * len(g)
    for s in range(len(g)):
        if color[s] != -1:
            continue
        color[s] = 0
        stack = [s]
        while stack:
            v = stack.pop()
            other = color[v] ^ 1
            for u in g[v]:
                if color[u] == -1:
                    color[u] = other
                    stack.append(u)
                elif color[u] != other:
                    return None
    return color
```

## 考え方

辺を渡るたび色を反転する。矛盾があれば奇数長の閉路がある。非連結なら各成分の色は独立に反転できる。

### 例題

```python
assert bipartite([[1], [0], []]) == [0, 1, 0]
assert bipartite([[1, 2], [0, 2], [0, 1]]) is None
```

[分野の目次](README.md) · [全体の目次](../README.md)
