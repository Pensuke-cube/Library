# 二部マッチング / Hopcroft–Karp Bipartite Matching

**4/5** · 左右の頂点を重複なく最大個数組にする。O((V+E)√V)。

## 使い方

bipartite_matching(g,right_size) の g[l] は対応可能な右頂点。戻り値は右頂点に割り当てた左頂点。未対応は -1。

## コード

```python
from collections import deque

def bipartite_matching(g, right_size):
    left = [-1] * len(g)
    right = [-1] * right_size
    free = [u for u, row in enumerate(g) if row]
    while free:
        dist = [-1] * len(g)
        q = deque(free)
        for u in free:
            dist[u] = 0
        shortest = len(g) + 1
        while q:
            u = q.popleft()
            depth = dist[u] + 1
            if depth > shortest:
                break
            for v in g[u]:
                match = right[v]
                if match < 0:
                    shortest = depth
                elif dist[match] < 0 and depth < shortest:
                    dist[match] = depth
                    q.append(match)
        if shortest > len(g):
            break

        cursor = [0] * len(g)
        for s in free:
            stack = [s]
            while stack:
                u = stack[-1]
                if cursor[u] == len(g[u]):
                    dist[u] = -1
                    stack.pop()
                    continue
                v = g[u][cursor[u]]
                cursor[u] += 1
                match = right[v]
                depth = dist[u] + 1
                if match < 0 and depth == shortest:
                    for node in reversed(stack):
                        right[v] = node
                        left[node], v = v, left[node]
                        dist[node] = -1
                    break
                if match >= 0 and depth < shortest and dist[match] == depth:
                    stack.append(match)
        free = [u for u in free if left[u] < 0]
    return right
```

## 考え方

未対応の左頂点から、未採用・採用の辺を交互に辿る。未対応の右頂点へ着いたら経路上の採否を反転すると 1 組増える。BFS で最短の増加路の長さを求め、その長さの増加路を一度の段階で複数使う。

### 例題

```python
assert bipartite_matching([[0,1], [0]], 2) == [1,0]
```

[分野の目次](README.md) · [全体の目次](../README.md)
