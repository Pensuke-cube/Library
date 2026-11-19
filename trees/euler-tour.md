# 木の根付き化・オイラーツアー / Rooting and Euler Tour

**5/5** · 部分木を連続区間に変換する。前処理 O(N)、区間取得 O(1)。

## 使い方

`root_tree(g, root=0)` に空でない無向木と、根にする頂点を渡す。`g[v]` は 0 始まりの頂点 `v` の隣接リスト。各辺は両方向を登録する。

- `parent[v]` は親（根だけ `-1`）、`depth[v]` は根から数えた辺数。
- `order` は DFS で最初に訪れた順の頂点列。頂点 `v` と全子孫は `order[tin[v]:tout[v]]` に入る。
- 戻り値の順は `(parent, depth, order, tin, tout)`。

## コード

```python
def root_tree(g, root=0):
    n = len(g)
    parent = [-1] * n
    depth = [0] * n
    tin, tout, order = [0]*n, [0]*n, []
    stack = [root]
    while stack:
        v = stack.pop()
        if v < 0:
            tout[~v] = len(order)
            continue
        tin[v] = len(order)
        order.append(v)
        stack.append(~v)
        for u in reversed(g[v]):
            if u != parent[v]:
                parent[u] = v
                depth[u] = depth[v] + 1
                stack.append(u)
    return parent, depth, order, tin, tout
```

## 考え方

入った時刻を記録し、全ての子の処理後に出る。部分木内の一点更新・区間和は DFS 順の Fenwick 木で扱える。

### 例題

```python
_, _, order, tin, tout = root_tree([[1,2], [0,3], [0], [1]])
assert order[tin[1]:tout[1]] == [1,3]
```

[分野の目次](README.md) · [全体の目次](../README.md)
