# 約数列挙・素因数分解・最小素因数 / Divisors, Factorization and Smallest Prime Factor

**5/5** · 単発を O(√N) で処理し、最小素因数表があれば分解を O(log N) 回の除算で行う。

## 使い方

- `divisors(n)` は正整数 `n` の正約数を昇順のリストで返す。
- `factorize(n, spf=None)` に正整数を渡すと `{素因数: 指数}` を返す。例えば 12 なら `{2: 2, 3: 1}`、1 なら空の辞書。
- 何度も分解する場合は `spf_table(limit)` に調べる整数の上限を渡す。結果の `spf[x]` は `2 <= x <= limit` で `x` の最小素因数。`factorize(n, spf)` として表を再利用する。`1 <= n <= limit`。

## コード

```python
from math import isqrt

def divisors(n):
    left, right = [], []
    for i in range(1, isqrt(n)+1):
        if n % i == 0:
            left.append(i)
            if i*i != n:
                right.append(n//i)
    return left + right[::-1]

def factorize(n, spf=None):
    factors = {}
    if spf is not None:
        while n > 1:
            p = spf[n]
            factors[p] = factors.get(p, 0) + 1
            n //= p
        return factors
    p = 2
    while p*p <= n:
        while n % p == 0:
            factors[p] = factors.get(p, 0) + 1
            n //= p
        p = 3 if p == 2 else p + 2
    if n > 1:
        factors[n] = 1
    return factors

def spf_table(limit):
    spf = list(range(limit+1))
    for p in range(2, isqrt(limit)+1):
        if spf[p] == p:
            for v in range(p*p, limit+1, p):
                if spf[v] == v:
                    spf[v] = p
    return spf
```

## 考え方

約数 i と n//i は対になる。素因数分解では割れなくなるまで除き、最後に残った値は素数。分解結果から約数個数は各 (指数+1) の積、φ(n) は各素因数 p について n に (p-1)/p を掛けて求める。

### 例題

```python
assert divisors(12) == [1,2,3,4,6,12]
assert factorize(72) == factorize(72, spf_table(100)) == {2:3,3:2}
```

[分野の目次](README.md) · [全体の目次](../README.md)
