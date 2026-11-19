# 巻き戻し Union-Find・動的連結性 / Rollback DSU and Offline Dynamic Connectivity

**3/5** · 連結成分の結合・判定を O(log N)、一回の結合の巻き戻しを O(1) で行う。

## 使い方

`RollbackDSU(n)` に要素数 `n` を渡す。要素番号は `0` から `n-1` で、最初はすべて別のグループ。

- `merge(a, b)` はグループを結合し、新たに結合したときだけ `True`。
- `leader(v)` は現在の代表番号。代表が同じなら連結している。
- `snapshot()` は現在の履歴位置を返す。`uf = RollbackDSU(n)` なら、結合前に `snap = uf.snapshot()` を記録し、後で `uf.rollback(snap)` を呼ぶとその時点までの状態へ戻る。

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
