# 素数判定・エラトステネスの篩 / Primality Test and Sieve of Eratosthenes

**5/5** · 単発の素数判定を O(√N)、N 以下の一括判定を O(N log log N) で行う。

## 使い方

- `is_prime_trial(n)` に整数を一つ渡す。`n` が素数なら `True`。2 未満なら `False`。
- `sieve(n)` に調べたい上限 `n`（0 以上の整数）を渡す。長さ `n+1` の `bytearray` を返し、`flags[x]` は `x` が素数なら 1、それ以外は 0。複数の値の判定に使い回せる。

## コード

```python
from math import isqrt

def is_prime_trial(n):
    if n < 2 or n % 2 == 0:
        return n == 2
    return all(n % d for d in range(3, isqrt(n)+1, 2))

def sieve(n):
    prime = bytearray(b"\x01") * (n+1)
    prime[:min(2, n+1)] = bytes(min(2, n+1))
    for p in range(2, isqrt(n)+1):
        if prime[p]:
            prime[p*p::p] = bytes((n-p*p)//p + 1)
    return prime
```

## 考え方

合成数には √N 以下の約数がある。篩では p の倍数のうち p² 未満は小さい素数で処理済み。巨大値の単発判定には Miller–Rabin 法を使う。

### 例題

```python
assert is_prime_trial(97) and not is_prime_trial(49)
assert [i for i, p in enumerate(sieve(11)) if p] == [2,3,5,7,11]
```

[分野の目次](README.md) · [全体の目次](../README.md)
