# 順序付き多重集合 / Ordered Multiset

**4/5** · 既知の値域で追加・削除・順位・k 番目を O(log M) で処理する。

## 使い方

[Fenwick 木](fenwick.md)のコードを先に置く。OrderedMultiset(values) に候補値を全て渡す。kth(k) は 0 始まり。存在する個数を超えて削除しない。

## コード

```python
from bisect import bisect_left, bisect_right

class OrderedMultiset:
    def __init__(self, values):
        self.values = sorted(set(values))
        self.index = {x: i for i, x in enumerate(self.values)}
        self.bit = Fenwick(len(self.values))

    def add(self, x, count=1):
        self.bit.add(self.index[x], count)

    def count_lt(self, x):
        return self.bit.prefix(bisect_left(self.values, x))

    def count_le(self, x):
        return self.bit.prefix(bisect_right(self.values, x))

    def kth(self, k):
        if k < 0:
            raise IndexError(k)
        return self.values[self.bit.lower_bound(k + 1)]
```

## 考え方

順位は圧縮値の手前までの度数和。最大の x 以下は kth(count_le(x)-1)。未知の値が追加される場合は環境にあれば sortedcontainers.SortedList も使える。

### 例題

```python
s = OrderedMultiset([1, 3, 8])
for x in [8, 1, 3, 3]:
    s.add(x)
assert s.count_lt(4) == 3 and s.kth(2) == 3
s.add(3, -1)
assert s.kth(2) == 8
```

[分野の目次](README.md) · [全体の目次](../README.md)
