# 最大公約数・最小公倍数・拡張 Euclid / GCD, LCM and Extended Euclidean Algorithm

**5/5** · 整数の GCD・LCM・Bézout 係数を O(log(min(

## 使い方

gcd(a,b)、lcm(a,b) は標準ライブラリ。extgcd(a,b) は g≥0 と ax+by=g を満たす (g,x,y)。

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
