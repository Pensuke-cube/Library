# 素集合データ構造・Union-Find / Disjoint Set Union

**5/5** · 併合・同じ連結成分かの判定を償却 O(α(N)) で行う。

## 使い方

DSU(n) を作り、merge(a,b) で結合。結合したとき True。same(a,b) と size(a) で問い合わせる。

## コード

```python
class DSU:
    def __init__(self, n):
        self.parent = [-1] * n

    def leader(self, x):
        p = self.parent
        while p[x] >= 0:
            if p[p[x]] >= 0:
                p[x] = p[p[x]]
            x = p[x]
        return x

    def merge(self, a, b):
        a, b = self.leader(a), self.leader(b)
        if a == b:
            return False
        p = self.parent
        if p[a] > p[b]:
            a, b = b, a
        p[a] += p[b]
        p[b] = a
        return True

    def same(self, a, b):
        return self.leader(a) == self.leader(b)

    def size(self, x):
        return -self.parent[self.leader(x)]
```

## 考え方

根に成分サイズの負値を置く。小さい木を大きい木につけ、探索した経路を縮める。無向辺の追加に向く。削除だけの列は時系列を逆にして追加に変えられる。

### 例題

```python
uf = DSU(4)
assert uf.merge(0, 1) and uf.merge(1, 3)
assert uf.same(0, 3) and uf.size(3) == 3
```

[分野の目次](README.md) · [全体の目次](../README.md)
