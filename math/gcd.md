# 最大公約数・最小公倍数・拡張 Euclid / GCD, LCM and Extended Euclidean Algorithm

**5/5** · 整数の GCD・LCM・Bézout 係数を O(log(min(

## 使い方

整数 `a`、`b` に対し、`gcd(a, b)` は非負の最大公約数、`lcm(a, b)` は非負の最小公倍数。`gcd(0, 0)` と、どちらかが 0 の `lcm` は 0。

`extgcd(a, b)` は `(g, x, y)` を返す。`g` は最大公約数、`x` と `y` は `a*x + b*y == g` を満たす整数。

## コード

```python
from math import gcd, lcm

def extgcd(a, b):
    x, y, u, v = 1, 0, 0, 1
    while b:
        q, r = divmod(a, b)
        a, b = b, r
        x, u = u, x-q*u
        y, v = v, y-q*v
    return (a, x, y) if a >= 0 else (-a, -x, -y)
```

## 考え方

余りに置き換えても共通の約数は同じ。拡張版は各余りを元の二数の一次結合として追跡する。ax+by=c の整数解が存在する条件は gcd(a,b) が c を割ること（両方 0 の場合は c=0）。

### 例題

```python
g, x, y = extgcd(30, -18)
assert g == 6 and 30*x - 18*y == g and lcm(30,18) == 90
```

[分野の目次](README.md) · [全体の目次](../README.md)
