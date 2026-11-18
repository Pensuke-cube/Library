# Fenwick 木・転倒数 / Fenwick Tree / Binary Indexed Tree

**5/5** · 一点加算・区間和・累積和の境界探索を O(log N) で行う。

## 使い方

Fenwick(n) の添字は 0 始まり。sum(l,r) は [l,r)。lower_bound(k) は累積和が k 以上になる最初の要素位置。全要素非負で k>0 のとき使う。該当なしは n。

## コード

```python
class Fenwick:
    def __init__(self, n):
        self.n = n
        self.data = [0] * (n + 1)

    def add(self, i, x):
        i += 1
        while i <= self.n:
            self.data[i] += x
            i += i & -i

    def prefix(self, r):
        total = 0
        while r:
            total += self.data[r]
            r -= r & -r
        return total

    def sum(self, l, r):
        return self.prefix(r) - self.prefix(l)

    def lower_bound(self, k):
        i = 0
        for bit in range(self.n.bit_length() - 1, -1, -1):
            j = i + (1 << bit)
            if j <= self.n and self.data[j] < k:
                k -= self.data[j]
                i = j
        return i
```

## 考え方

内部の 1 始まり添字 i は末尾の 1 ビットが表す長さの区間和を持つ。転倒数は各値を圧縮し、左側にある自分より大きい値の個数を足す。

### 例題

```python
a = [3, 1, 2, 1]
rank = {x: i for i, x in enumerate(sorted(set(a)))}
fw = Fenwick(len(rank))
inversions = 0
for i, x in enumerate(a):
    r = rank[x]
    inversions += i - fw.prefix(r + 1)
    fw.add(r, 1)
assert inversions == 4 and fw.lower_bound(3) == 1
```

[分野の目次](README.md) · [全体の目次](../README.md)
