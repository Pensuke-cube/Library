# 中国剰余定理 / Chinese Remainder Theorem

**4/5** · 複数の合同式を併合し、最小非負解と周期を求める。

## 使い方

`crt(pairs)` に `(r, m)` の列を渡す。各組は「求めたい整数 `x` を正整数 `m` で割ると `r` と合同」という条件で、`r` は負でもよい。全条件を満たす最小の非負整数 `x` と解の周期 `period` を `(x, period)` で返す。矛盾があれば `None`。全解は `x + k*period`（`k` は任意の整数）。

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
