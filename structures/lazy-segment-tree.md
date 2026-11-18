# 遅延セグメント木 / Lazy Segment Tree

**5/5** · 区間更新と区間集約を O(log N) で行う。

## 使い方

LazySeg(a,op,e,apply,compose,id_)。apply(f,x) は集約値 x に更新 f を作用させる。compose(f,g) は g の後に f を適用。range_apply(l,r,f)、prod(l,r) は半開区間。set(i,x) は一点代入。

## コード

```python
class LazySeg:
    def __init__(self, a, op, e, apply, compose, id_):
        self.op, self.e = op, e
        self.apply, self.compose, self.id = apply, compose, id_
        self.log = (max(1, len(a)) - 1).bit_length()
        self.size = size = 1 << self.log
        self.data = d = [e] * (2 * size)
        self.lazy = [id_] * size
        d[size:size + len(a)] = a
        for i in range(size - 1, 0, -1):
            self._pull(i)

    def _pull(self, i):
        d = self.data
        d[i] = self.op(d[i * 2], d[i * 2 + 1])

    def _apply(self, i, f):
        self.data[i] = self.apply(f, self.data[i])
        if i < self.size:
            self.lazy[i] = self.compose(f, self.lazy[i])

    def _push(self, i):
        f = self.lazy[i]
        if f != self.id:
            self._apply(i * 2, f)
            self._apply(i * 2 + 1, f)
            self.lazy[i] = self.id

    def _push_edges(self, l, r):
        for i in range(self.log, 0, -1):
            if l >> i << i != l:
                self._push(l >> i)
            if r >> i << i != r:
                self._push((r - 1) >> i)

    def range_apply(self, l, r, f):
        if l == r:
            return
        l, r = l + self.size, r + self.size
        self._push_edges(l, r)
        left, right = l, r
        while l < r:
            if l & 1:
                self._apply(l, f)
                l += 1
            if r & 1:
                r -= 1
                self._apply(r, f)
            l >>= 1
            r >>= 1
        for i in range(1, self.log + 1):
            if left >> i << i != left:
                self._pull(left >> i)
            if right >> i << i != right:
                self._pull((right - 1) >> i)

    def set(self, i, x):
        i += self.size
        for k in range(self.log, 0, -1):
            self._push(i >> k)
        self.data[i] = x
        for k in range(1, self.log + 1):
            self._pull(i >> k)

    def prod(self, l, r):
        if l == r:
            return self.e
        l, r = l + self.size, r + self.size
        self._push_edges(l, r)
        left = right = self.e
        while l < r:
            if l & 1:
                left = self.op(left, self.data[l])
                l += 1
            if r & 1:
                r -= 1
                right = self.op(self.data[r], right)
            l >>= 1
            r >>= 1
        return self.op(left, right)
```

## 考え方

ノード全体への更新は集約値に反映し、子への伝播を後回しにする。区間和に加算するにはノードの長さも持つ。各更新は集約に分配できる形にする。例えば x→ax+b の合成は (a,b)∘(c,d)=(ac,ad+b)。

### 例題

```python
def combine(x, y):
    return x[0] + y[0], x[1] + y[1]

def apply(f, x):
    return f[0] * x[0] + f[1] * x[1], x[1]

def compose(f, g):
    return f[0] * g[0], f[0] * g[1] + f[1]

st = LazySeg([(1, 1), (2, 1), (3, 1)], combine, (0, 0), apply, compose, (1, 0))
st.range_apply(0, 2, (2, 1))
st.range_apply(1, 3, (0, 4))
assert st.prod(0, 3) == (11, 3)
st.set(1, (5, 1))
assert st.prod(0, 3) == (12, 3)
```

[分野の目次](README.md) · [全体の目次](../README.md)
