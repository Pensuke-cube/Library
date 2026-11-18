# 切り上げ・等差数列・整数平方根 / Integer Division and Arithmetic Progressions

**5/5** · 整数だけで商の丸め、等差数列の和、平方根の切り捨てを求める。

## 使い方

ceil_div(a,b) は b≠0。arithmetic_sum(first,step,n) は n 項の和。isqrt(n) は n≥0。

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
