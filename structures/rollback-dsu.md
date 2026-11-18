# 巻き戻し Union-Find・動的連結性 / Rollback DSU and Offline Dynamic Connectivity

**3/5** · 連結成分の結合・判定を O(log N)、一回の結合の巻き戻しを O(1) で行う。

## 使い方

snapshot() を取り、merge(a,b) を実行し、rollback(snap) で戻す。leader の一致で連結を調べる。

## コード

```python
class RollbackDSU:
    def __init__(self, n):
        self.p = [-1] * n
        self.history = []

    def leader(self, v):
        while self.p[v] >= 0:
            v = self.p[v]
        return v

    def merge(self, a, b):
        a, b = self.leader(a), self.leader(b)
        if a == b:
            return False
        p = self.p
        if p[a] > p[b]:
            a, b = b, a
        self.history.append((a, p[a], b, p[b]))
        p[a] += p[b]
        p[b] = a
        return True

    def snapshot(self):
        return len(self.history)

    def rollback(self, snap):
        while len(self.history) > snap:
            a, pa, b, pb = self.history.pop()
            self.p[a], self.p[b] = pa, pb
```

## 考え方

サイズ順の結合だけで深さを O(log N) に保つ。動的連結性では各辺の有効期間を時刻のセグメント木に分解し、DFS 中にノードの辺を結合、退出時に巻き戻す。辺の有効区間が M 個なら結合の費用は O(M log Q log N)。

### 例題

```python
d = RollbackDSU(3)
d.merge(0, 1)
snap = d.snapshot()
d.merge(1, 2)
assert d.leader(0) == d.leader(2)
d.rollback(snap)
assert d.leader(0) != d.leader(2) and d.leader(0) == d.leader(1)
```

[分野の目次](README.md) · [全体の目次](../README.md)
