# トポロジカルソート・DAG DP / Topological Sort and DAG DP

**5/5** · 依存関係を守る順序を O(V+E) で求め、有向閉路を検出する。

## 使い方

`toposort(g)` の `g[u]` に頂点 `u` から出る有向辺の行き先を並べる。頂点番号は 0 始まり。辺 `u → v` ごとに `u` が `v` より先に来る頂点リストを返す。そのように並べられない場合は `None`。辞書順最小が必要ならコード中のキューを最小ヒープに替える。

## コード

```python
from collections import deque

def toposort(g):
    n = len(g)
    indegree = [0] * n
    for row in g:
        for v in row:
            indegree[v] += 1
    q = deque(v for v in range(n) if indegree[v] == 0)
    order = []
    while q:
        v = q.popleft()
        order.append(v)
        for u in g[v]:
            indegree[u] -= 1
            if indegree[u] == 0:
                q.append(u)
    return order if len(order) == n else None
```

## 考え方

入次数 0 の頂点を先に取り除く。DAG 上の経路数や最長路は、全ての前駆頂点の処理が済んだ順に更新する。

### 例題

```python
g = [[1, 2], [3], [3], []]
ways = [1, 0, 0, 0]
for v in toposort(g):
    for u in g[v]:
        ways[u] += ways[v]
assert ways[3] == 2 and toposort([[1], [0]]) is None
```

[分野の目次](README.md) · [全体の目次](../README.md)
