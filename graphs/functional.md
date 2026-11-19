# 関数グラフ・閉路と流入木 / Functional Graph

**4/5** · 各頂点が一つの行き先を持つグラフで、閉路の長さと閉路までの距離を O(N) で求める。

## 使い方

`functional_graph(nxt)` に全頂点の行き先を並べたリストを渡す。`nxt[v]` は `v` が一歩で進む頂点で、各値は `0` から `len(nxt)-1`。`(distance, length)` を返す。`distance[v]` は閉路に初めて入るまでの歩数、`length[v]` はその閉路の頂点数。

## コード

```python
from collections import deque

def functional_graph(nxt):
    n = len(nxt)
    degree = [0] * n
    for v in nxt:
        degree[v] += 1
    q = deque(v for v in range(n) if degree[v] == 0)
    order = []
    while q:
        v = q.popleft()
        order.append(v)
        u = nxt[v]
        degree[u] -= 1
        if degree[u] == 0:
            q.append(u)
    distance, length = [0]*n, [0]*n
    for s in range(n):
        if not degree[s] or length[s]:
            continue
        cycle = [s]
        v = nxt[s]
        while v != s:
            cycle.append(v)
            v = nxt[v]
        for v in cycle:
            length[v] = len(cycle)
    for v in reversed(order):
        u = nxt[v]
        length[v] = length[u]
        distance[v] = distance[u] + 1
    return distance, length
```

## 考え方

入次数 0 を繰り返し取り除くと閉路だけが残る。除いた順を逆に辿れば行き先の答えが決まっている。各始点から訪問する異なる頂点数は距離と閉路長の和。

### 例題

```python
assert functional_graph([1,2,1,2,4]) == ([1,0,0,1,0], [2,2,2,2,1])
```

[分野の目次](README.md) · [全体の目次](../README.md)
