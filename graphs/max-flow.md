# 最大流・最小カット / Maximum Flow and Minimum Cut / Dinic

**4/5** · 有向容量つきの最大流と最小カットを求める。一般計算量 O(V²E)。

## 使い方

`Dinic(n)` で頂点数 `n` の空グラフを作る。頂点番号は `0` から `n-1`。

- `add(a, b, cap)` は `a` から `b` への有向辺を追加する。`cap` は非負整数の容量。両向きに容量があるなら別々に追加する。
- `flow(s, t)` は異なる始点 `s` と終点 `t` の間で、今の状態から追加で流せる最大量を返し、内部の流量を更新する。最初の呼び出しでは最大流量が得られる。
- `reachable(s)` は残り容量のある辺で `s` から届く頂点の集合。最大流の計算後なら最小カットの始点側。

## コード

```python
from collections import deque

class Dinic:
    def __init__(self, n):
        self.g = [[] for _ in range(n)]

    def add(self, a, b, cap):
        g = self.g
        forward = [b, cap, None]
        reverse = [a, 0, forward]
        forward[2] = reverse
        g[a].append(forward)
        g[b].append(reverse)

    def flow(self, s, t):
        g = self.g
        n = len(g)
        total = 0
        while True:
            level = [-1] * n
            level[s] = 0
            q = deque([s])
            while q:
                v = q.popleft()
                for u, cap, _ in g[v]:
                    if cap and level[u] < 0:
                        level[u] = level[v] + 1
                        q.append(u)
            if level[t] < 0:
                return total

            it = [0] * n
            path = []
            v = s
            while True:
                if v == t:
                    amount = min(edge[1] for _, edge in path)
                    total += amount
                    for _, edge in path:
                        edge[1] -= amount
                        edge[2][1] += amount
                    v = s
                    path.clear()
                    continue
                if it[v] == len(g[v]):
                    level[v] = -1
                    if not path:
                        break
                    v, _ = path.pop()
                    it[v] += 1
                    continue
                edge = g[v][it[v]]
                u, cap, _ = edge
                if cap and level[u] == level[v] + 1:
                    path.append((v, edge))
                    v = u
                else:
                    it[v] += 1

    def reachable(self, s):
        reached = {s}
        q = [s]
        for v in q:
            for u, cap, _ in self.g[v]:
                if cap and u not in reached:
                    reached.add(u)
                    q.append(u)
        return reached
```

## 考え方

残余辺は追加で流せる量と逆向きに取り消せる量を表す。BFS の層を一つずつ進む経路だけを使い、層内の流せる道を全て使ってから層を作り直す。最大流後に s から残余辺で辿れる集合がカットの始点側。

### 例題

```python
f = Dinic(4)
for a, b, c in [(0,1,3), (0,2,2), (1,3,2), (2,3,3), (1,2,1)]:
    f.add(a, b, c)
assert f.flow(0, 3) == 5 and f.reachable(0) == {0}
```

[分野の目次](README.md) · [全体の目次](../README.md)
