# 二分探索・答えで二分探索 / Binary Search

**5/5** · 整列済み配列の境界や単調な判定が切り替わる点を O(log N) 回で探す。

## 使い方

- `first_true(lo, hi, ok)` に整数の探索範囲 `[lo, hi)` と、整数を受け取って真偽を返す関数 `ok(x)` を渡す。判定は範囲内で偽から真へ切り替わり、一度真になれば後も真。最初に真となる整数を返し、一つもなければ `hi`。
- 昇順リスト `a` なら `bisect_left(a, x)` は `x` 以上、`bisect_right(a, x)` は `x` より大きい最初の添字。該当する要素がなければ `len(a)`。

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
