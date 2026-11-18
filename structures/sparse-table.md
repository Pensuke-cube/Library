# スパーステーブル / Sparse Table

**4/5** · 変更のない列を O(N log N) で前処理し、区間最小・最大・GCD を O(1) で求める。

## 使い方

SparseTable(a,op).prod(l,r) は空でない [l,r) を集約。op は結合則と op(x,x)=x を満たす。

## コード

```python
class SparseTable:
    def __init__(self, a, op=min):
        self.op = op
        self.table = [list(a)]
        k = 1
        while 2 * k <= len(a):
            prev = self.table[-1]
            self.table.append([op(prev[i], prev[i+k]) for i in range(len(a)-2*k+1)])
            k *= 2

    def prod(self, l, r):
        k = (r - l).bit_length() - 1
        row = self.table[k]
        return self.op(row[l], row[r - (1 << k)])
```

## 考え方

2 のべき乗長の区間値を記録する。クエリを両端から最大長の二つで覆うため、重複が結果に影響しない演算を選ぶ。

### 例題

```python
assert SparseTable([4, 2, 5, 1]).prod(0, 3) == 2
```

[分野の目次](README.md) · [全体の目次](../README.md)
