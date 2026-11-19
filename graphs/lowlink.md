# 橋・関節点 / Bridges and Articulation Points / Lowlink

**3/5** · 無向グラフの橋と関節点を O(V+E) で求める。多重辺可。

## 使い方

`lowlink(n, edges)` に頂点数 `n` と無向辺 `(u, v)` の列を渡す。頂点番号は `0` から `n-1`、辺番号は入力順の 0 始まり。多重辺も別の番号で扱う。`(bridges, cuts)` を返し、`bridges` は取り除くと連結成分数が増える辺の番号、`cuts` は取り除くと連結成分数が増える頂点の番号。

## コード

```python
def lowlink(n, edges):
    g = [[] for _ in range(n)]
    for i, (a, b) in enumerate(edges):
        g[a].append((b, i))
        g[b].append((a, i))
    order = [-1] * n
    low = [0] * n
    cut = bytearray(n)
    bridges = []
    timer = 0
    for s in range(n):
        if order[s] >= 0:
            continue
        order[s] = low[s] = timer
        timer += 1
        children = 0
        stack = [(s, -1, iter(g[s]))]
        while stack:
            v, edge, it = stack[-1]
            item = next(it, None)
            if item is None:
                stack.pop()
                if stack:
                    p = stack[-1][0]
                    low[p] = min(low[p], low[v])
                    if low[v] > order[p]:
                        bridges.append(edge)
                    if len(stack) > 1 and low[v] >= order[p]:
                        cut[p] = 1
                continue
            u, i = item
            if i == edge:
                continue
            if order[u] >= 0:
                low[v] = min(low[v], order[u])
                continue
            if v == s:
                children += 1
            order[u] = low[u] = timer
            timer += 1
            stack.append((u, i, iter(g[u])))
        cut[s] = children >= 2
    return bridges, [v for v in range(n) if cut[v]]
```

## 考え方

low[v] は部分木から木辺と後退辺で届く最古の訪問番号。親 p より先に戻れないと p が関節点の候補になり、p 自体にも戻れなければその辺は橋。根だけは DFS の子が 2 個以上かで判定する。

### 例題

```python
bridges, cuts = lowlink(3, [(0,1), (0,1), (1,2)])
assert bridges == [2] and cuts == [1]
```

[分野の目次](README.md) · [全体の目次](../README.md)
