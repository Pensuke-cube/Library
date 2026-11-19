# 切り上げ・等差数列・整数平方根 / Integer Division and Arithmetic Progressions

**5/5** · 整数だけで商の丸め、等差数列の和、平方根の切り捨てを求める。

## 使い方

- `ceil_div(a, b)` に整数 `a` と 0 でない整数 `b` を渡す。`a/b` 以上の最小整数を返す。
- `arithmetic_sum(first, step, n)` に初項 `first`、隣り合う項の差 `step`、項数 `n`（0 以上）を整数で渡す。先頭 `n` 項の和を返す。
- `isqrt(n)` に非負整数を渡し、二乗が `n` 以下になる最大の非負整数を得る。

## コード

```python
from math import isqrt

def ceil_div(a, b):
    return -(-a // b)

def arithmetic_sum(first, step, n):
    return n * (2*first + (n-1)*step) // 2
```

## 考え方

Python の // は負の無限大方向へ丸める。ceil は符号を反転して床関数を取ればよい。等差数列は初項と末項の平均に項数を掛ける。浮動小数点を通すと大きい値で厳密性が落ちる。

### 例題

```python
assert ceil_div(11,3) == 4 and ceil_div(-11,3) == -3
assert arithmetic_sum(2,3,4) == 26 and isqrt(10**36-1) == 10**18-1
```

[分野の目次](README.md) · [全体の目次](../README.md)
