# マージソート木・静的区間順位 / Merge Sort Tree

**3/5** · 静的な区間内の閾値以下の個数を O(log² N) で求める。構築 O(N log N)。

## 使い方

`MergeSortTree(a)` に順序比較できる値の列を渡して前計算する。`count_le(l, r, x)` に `0 <= l <= r <= len(a)` と比較する値 `x` を渡すと、`a[l:r]` にある `x` 以下の要素数を返す。同じ値も位置ごとに数える。

## コード

```python
from bisect import bisect_right
from heapq import merge

class MergeSortTree:
    def __init__(self, a):
        self.n = n = len(a)
        d = [[] for _ in range(n)] + [[x] for x in a]
        for i in range(n-1,0,-1):
            d[i] = list(merge(d[2*i], d[2*i+1]))
        self.data = d

    def count_le(self, l, r, x):
        l, r = l+self.n, r+self.n
        cnt = 0
        while l < r:
            if l & 1:
                cnt += bisect_right(self.data[l],x)
                l += 1
            if r & 1:
                r -= 1
                cnt += bisect_right(self.data[r],x)
            l >>= 1
            r >>= 1
        return cnt
```

## 考え方

各ノードに値の昇順リストを置く。通常の区間取得と同じ範囲分解を行い、各リストで二分探索する。全クエリが先に分かるなら閾値順に処理する方法の方が軽い。

### 例題

```python
m = MergeSortTree([8,1,5,3,4])
assert m.count_le(1,4,3) == 2 and m.count_le(2,2,10) == 0
```

[分野の目次](README.md) · [全体の目次](../README.md)
