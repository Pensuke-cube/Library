# 単峰探索 / Unimodal Search

**3/5** · 離散凸関数の最小位置を O(log N) 回の評価で探す。

## 使い方

`argmin_convex(lo, hi, f)` に両端を含む整数範囲 `[lo, hi]` と、位置 `i` での値を返す関数 `f(i)` を渡す。`lo <= hi` で、隣接差 `f(i+1)-f(i)` が非減少であること。最小値を取る添字を返し、同値なら最も左を選ぶ。

## コード

```python
def argmin_convex(lo, hi, f):
    while lo < hi:
        mid = (lo + hi) // 2
        if f(mid) <= f(mid + 1):
            hi = mid
        else:
            lo = mid + 1
    return lo
```

## 考え方

隣り合う値を比較することで傾きの符号が変わる点を求める。同値が続いた後でさらに下降するような関数には使えない。

### 例題

```python
assert argmin_convex(-10, 10, lambda x: (x-3)**2) == 3
```

[分野の目次](README.md) · [全体の目次](../README.md)
