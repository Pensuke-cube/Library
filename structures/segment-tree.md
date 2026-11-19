# セグメント木 / Segment Tree

**5/5** · 一点代入・区間集約・区間の右境界探索を O(log N) で行う。

## 使い方

`SegTree(a, op, e)` に初期値の列 `a`（長さ `n`）、集約関数 `op(x, y)`、空区間の値 `e` を渡す。左・右の値をその順で結合し、結合順の括り方で結果が変わらないこと。例は和なら `op=int.__add__`・`e=0`。

- `set(i, x)` は `0 <= i < n` の要素を `x` に置き換える。`prod(l, r)` は `[l, r)` を集約する。`0 <= l <= r <= n`。
- `max_right(l, ok)` は `ok(prod(l, r))` が真になる最大の `r`。`min_left(r, ok)` は真になる最小の `l`。`ok(value)` は真偽を返す関数で、`ok(e)` は真。区間を延ばして一度偽になったら後も偽であること。

## コード

```python
class SegTree:
    def __init__(self, a, op, e):
        self.n, self.op, self.e = len(a), op, e
        self.size = size = 1 << max(0, (len(a) - 1).bit_length())
        d = [e] * (2 * size)
        d[size:size + len(a)] = a
        for i in range(size - 1, 0, -1):
            d[i] = op(d[i * 2], d[i * 2 + 1])
        self.data = d

    def set(self, i, x):
        i += self.size
        d, op = self.data, self.op
        d[i] = x
        while i > 1:
            i >>= 1
            d[i] = op(d[i * 2], d[i * 2 + 1])

    def prod(self, l, r):
        l, r = l + self.size, r + self.size
        left = right = self.e
        d, op = self.data, self.op
        while l < r:
            if l & 1:
                left = op(left, d[l])
                l += 1
            if r & 1:
                r -= 1
                right = op(d[r], right)
            l >>= 1
            r >>= 1
        return op(left, right)

    def max_right(self, l, ok):
        if l == self.n:
            return l
        d, op = self.data, self.op
        l += self.size
        value = self.e
        while True:
            while l % 2 == 0:
                l >>= 1
            candidate = op(value, d[l])
            if not ok(candidate):
                while l < self.size:
                    l *= 2
                    candidate = op(value, d[l])
                    if ok(candidate):
                        value = candidate
                        l += 1
                return l - self.size
            value = candidate
            l += 1
            if l & -l == l:
                return self.n

    def min_left(self, r, ok):
        if r == 0:
            return 0
        d, op = self.data, self.op
        r += self.size
        value = self.e
        while True:
            r -= 1
            while r > 1 and r & 1:
                r >>= 1
            candidate = op(d[r], value)
            if not ok(candidate):
                while r < self.size:
                    r = r*2 + 1
                    candidate = op(d[r], value)
                    if ok(candidate):
                        value = candidate
                        r -= 1
                return r + 1 - self.size
            value = candidate
            if r & -r == r:
                return 0
```

## 考え方

区間を木のノードに分解する。行列積や文字列結合では順序が重要なので左右を別に集約する。境界探索は条件を壊すノードを見つけ、その子へ降りる。

### 例題

```python
st = SegTree([2, 1, 4, 3], max, -float("inf"))
assert st.prod(1, 3) == 4 and st.max_right(1, lambda x: x < 4) == 2
assert st.min_left(4, lambda x: x < 4) == 3
st.set(2, 0)
assert st.prod(1, 3) == 1
```

[分野の目次](README.md) · [全体の目次](../README.md)
