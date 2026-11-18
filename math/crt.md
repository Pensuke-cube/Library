# 中国剰余定理 / Chinese Remainder Theorem

**4/5** · 複数の合同式を併合し、最小非負解と周期を求める。

## 使い方

crt(pairs) は (余り,正の法) を受け取り (解,周期) を返す。矛盾なら None。

## コード

```python
from math import gcd

def crt(pairs):
    r, m = 0, 1
    for s, n in pairs:
        d = gcd(m, n)
        diff = s-r
        if diff % d:
            return None
        q = n//d
        if q > 1:
            r += m * (diff//d * pow(m//d, -1, q) % q)
            m *= q
    return r, m
```

## 考え方

既知の解を r+mt とおく。mt≡s-r (mod n) を最大公約数で割り、逆元を用いて t を決める。各併合は O(log 法) 回の除算が目安。周期自体が大きくなる場合は整数の桁数も効く。

### 例題

```python
assert crt([(2,6), (5,9)]) == (14,18)
assert crt([(0,2), (1,4)]) is None
```

[分野の目次](README.md) · [全体の目次](../README.md)
