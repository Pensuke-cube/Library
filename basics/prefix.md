# 累積和・二次元累積和 / Prefix Sums

**5/5** · 前処理 O(N) または O(HW) の後、区間和や長方形和を O(1) で求める。

## 使い方

p[r]-p[l] は [l,r)。rect_sum の座標は上端、左端、下端、右端で半開区間。

## コード

```python
from itertools import accumulate

def prefix_sum(a):
    return list(accumulate(a, initial=0))

def prefix_2d(a):
    h, w = len(a), len(a[0]) if a else 0
    p = [[0] * (w + 1) for _ in range(h + 1)]
    for i, row in enumerate(a):
        s = 0
        for j, x in enumerate(row):
            s += x
            p[i + 1][j + 1] = p[i][j + 1] + s
    return p

def rect_sum(p, top, left, bottom, right):
    return p[bottom][right] - p[top][right] - p[bottom][left] + p[top][left]
```

## 考え方

先頭に 0 を置くと l=0 でも式が同じ。二次元では上下左右のはみ出しを引き、左上の二重減算を戻す。XOR でも同様に範囲差を取れる。

### 例題

```python
p = prefix_sum([3, 1, 4, 1])
assert p[3] - p[1] == 5
assert rect_sum(prefix_2d([[1, 2], [3, 4]]), 0, 1, 2, 2) == 6
```

[分野の目次](README.md) · [全体の目次](../README.md)
