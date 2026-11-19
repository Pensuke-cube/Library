# 最小費用流 / Minimum-Cost Flow

**3/5** · 指定量まで流す最小費用を求める。最短路探索 K 回で O(K(V+E log(E+1)))。

## 使い方

`MinCostFlow(n)` で頂点数 `n` の空グラフを作る。頂点番号は `0` から `n-1`。

- `add(u, v, cap, cost)` は `u` から `v` への有向辺を追加する。`cap` は容量、`cost` は流量 1 当たりの費用。ともに非負整数。
- `flow(s, t, limit)` に異なる始点・終点と非負整数の目標流量を渡す。`(実際に流せた量, その流量の最小総費用)` を返す。目標まで流せなければ可能な最大量。流量を内部に記録するため、この実装では一つのインスタンスにつき一度だけ呼ぶ。

## コード

```python
from heapq import heappop, heappush

class MinCostFlow:
    def __init__(self, n):
        self.g = [[] for _ in range(n)]

    def add(self, u, v, cap, cost):
        edge = [v, cap, cost, None]
        reverse = [u, 0, -cost, edge]
        edge[3] = reverse
        self.g[u].append(edge)
        self.g[v].append(reverse)

    def flow(self, s, t, limit):
        g = self.g
        n = len(g)
        potential = [0] * n
        inf = float("inf")
        sent = total = 0
        while sent < limit:
            d = [inf] * n
            prev = [None] * n
            d[s] = 0
            heap = [(0, s)]
            while heap:
                dv, v = heappop(heap)
                if dv != d[v]:
                    continue
                for edge in g[v]:
                    u, cap, cost, _ = edge
                    nd = dv + cost + potential[v] - potential[u]
                    if cap and nd < d[u]:
                        d[u] = nd
                        prev[u] = (v, edge)
                        heappush(heap, (nd, u))
            if d[t] == inf:
                break
            for v, dv in enumerate(d):
                if dv != inf:
                    potential[v] += dv
            amount = limit - sent
            v = t
            while v != s:
                v, edge = prev[v]
                amount = min(amount, edge[1])
            v = t
            while v != s:
                v, edge = prev[v]
                edge[1] -= amount
                edge[3][1] += amount
            sent += amount
            total += amount * (potential[t] - potential[s])
        return sent, total
```

## 考え方

残余グラフの最安経路に流す。ポテンシャル差を費用に加えると経路同士の大小は変わらず、到達可能な辺の換算費用を非負に保てる。利益最大化の割当では、選ぶ件数が固定なら十分大きい値から利益を引く。

### 例題

```python
f = MinCostFlow(3)
f.add(0, 1, 2, 1)
f.add(1, 2, 2, 2)
f.add(0, 2, 3, 5)
assert f.flow(0, 2, 3) == (3, 11)
```

[分野の目次](README.md) · [全体の目次](../README.md)
