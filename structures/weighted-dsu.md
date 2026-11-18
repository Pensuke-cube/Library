# 重み付き Union-Find / Potentialized Union-Find

**4/5** · 差分制約 x[b]-x[a]=w の追加と照会を償却 O(α(N)) で行う。

## 使い方

merge(a,b,w) は制約と整合するなら True。diff(a,b) は差、未連結なら None。

## コード

```python
class WeightedDSU:
    def __init__(self, n):
        self.p = [-1] * n
        self.w = [0] * n

    def leader(self, x):
        p, w = self.p, self.w
        if p[x] < 0:
            return x
        old = p[x]
        root = self.leader(old)
        w[x] += w[old]
        p[x] = root
        return root

    def merge(self, a, b, delta):
        x, y = self.leader(a), self.leader(b)
        delta += self.w[a] - self.w[b]
        if x == y:
            return delta == 0
        p = self.p
        if p[x] > p[y]:
            x, y = y, x
            delta = -delta
        p[x] += p[y]
        p[y] = x
        self.w[y] = delta
        return True

    def diff(self, a, b):
        if self.leader(a) != self.leader(b):
            return None
        return self.w[b] - self.w[a]
```

## 考え方

各頂点に親との差を持たせる。経路圧縮では親までの差と親から根までの差を足す。同一成分では新しい差が既存の差と一致するか判定する。

### 例題

```python
d = WeightedDSU(4)
assert d.merge(0, 1, 6) and d.merge(2, 1, 2)
assert d.diff(0, 2) == 4 and d.diff(0, 3) is None
assert not d.merge(0, 2, 3)
```

[分野の目次](README.md) · [全体の目次](../README.md)
