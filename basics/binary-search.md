# 二分探索・答えで二分探索 / Binary Search

**5/5** · 整列済み配列の境界や単調な判定が切り替わる点を O(log N) 回で探す。

## 使い方

first_true(lo, hi, ok) は [lo, hi) の最初の真を返す。なければ hi。ok は偽→真の順。

## コード

```python
from bisect import bisect_left, bisect_right

def first_true(lo, hi, ok):
    while lo < hi:
        mid = (lo + hi) // 2
        if ok(mid):
            hi = mid
        else:
            lo = mid + 1
    return lo
```

## 考え方

bisect_left は x 以上、bisect_right は x より大きい最初の位置。答えを直接求めづらければ「値 x で実現可能か」を考える。実数は上下限を固定回数更新する。

### 例題

```python
# x² ≥ 50 を満たす最小の非負整数。
assert first_true(0, 51, lambda x: x*x >= 50) == 8
assert bisect_left([1, 3, 3, 5], 3) == 1
```

[分野の目次](README.md) · [全体の目次](../README.md)
