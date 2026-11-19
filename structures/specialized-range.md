# 区間加算・区間和の専用 Fenwick 木 / Range Add and Range Sum with Two Fenwick Trees

**4/5** · 区間加算と区間和を O(log N) で行う。集約・作用のコールバックを使わない。

## 使い方

[Fenwick 木](fenwick.md)のコードを先に置く。`RangeAddSum(n)` で長さ `n` の全要素 0 の配列を作る。

- `add(l, r, x)` は `[l, r)` の全要素に `x` を足す。`x` は負でも可。
- `sum(l, r)` は `[l, r)` の和、`prefix(r)` は先頭 `r` 個の和。`add` と `sum` は `0 <= l <= r <= n`、`prefix` は `0 <= r <= n`。

## コード

```python
class RangeAddSum:
    def __init__(self, n):
        self.diff = Fenwick(n+1)
        self.weighted = Fenwick(n+1)

    def add(self, l, r, x):
        self.diff.add(l, x)
        self.diff.add(r, -x)
        self.weighted.add(l, l*x)
        self.weighted.add(r, -r*x)

    def prefix(self, r):
        return r*self.diff.prefix(r) - self.weighted.prefix(r)

    def sum(self, l, r):
        return self.prefix(r) - self.prefix(l)
```

## 考え方

差分 d[i] は先頭 r 個の総和に r-i 回寄与する。r·Σd[i]-Σi·d[i] に分けて二本の木で管理する。加算と和に固定できるときに汎用遅延セグメント木の代わりに使える。

### 例題

```python
st = RangeAddSum(4)
st.add(0,3,2)
st.add(1,4,5)
assert st.sum(1,4) == 19
```

[分野の目次](README.md) · [全体の目次](../README.md)
