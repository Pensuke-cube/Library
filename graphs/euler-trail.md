# オイラー路 / Eulerian Trail / Hierholzer

**3/5** · 全ての辺を一度ずつ通る経路を O(V+E) で復元する。

## 使い方

`euler_trail(n, edges)` に頂点数 `n >= 1` と無向辺の列 `(u, v)` を渡す。頂点番号は `0` から `n-1`。多重辺は別々に並べる。全辺を一度ずつ通る順番を頂点のリストで返し、閉路なら先頭と末尾は同じ。解がなければ `None`、辺がなければ `[0]`。

## コード

```python
def euler_trail(n, edges):
    edges = list(edges)
    g = [[] for _ in range(n)]
    for i, (a, b) in enumerate(edges):
        g[a].append((b, i))
        g[b].append((a, i))
    odd = [v for v, row in enumerate(g) if len(row) & 1]
    if len(odd) not in (0, 2):
        return None
    start = odd[0] if odd else next((v for v in range(n) if g[v]), 0)
    stack, route = [start], []
    used = bytearray(len(edges))
    while stack:
        v = stack[-1]
        if not g[v]:
            route.append(stack.pop())
            continue
        u, i = g[v].pop()
        if not used[i]:
            used[i] = 1
            stack.append(u)
    return route[::-1] if len(route) == len(edges) + 1 else None
```

## 考え方

奇数次数の頂点が 2 個なら両端、0 個なら閉路になる。辿れる辺を進み、行き止まりの頂点から逆順に確定する。孤立点を除いた連結性も必要。

### 例題

```python
assert euler_trail(3, [(0,1), (1,2)]) == [0,1,2]
assert euler_trail(4, [(0,1), (0,1), (2,3), (2,3)]) is None
```

[分野の目次](README.md) · [全体の目次](../README.md)
