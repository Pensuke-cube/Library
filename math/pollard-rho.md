# ポラードのρ法・64 ビット素因数分解 / Pollard's Rho Factorization

**3/5** · 64 ビット整数を素因数分解する。素因数 p の発見は O(√p) 回の反復が目安。

## 使い方

[Miller–Rabin](miller-rabin.md)のコードを先に置く。`factor64(n, seed=0)` に `1 <= n < 2**64` の整数を渡す。積が `n` になる素因数の昇順リストを返し、同じ素因数は指数の回数だけ並ぶ。`n=1` なら `[]`。`seed` は分解に使う乱数の種。

## コード

```python
from math import gcd
from random import Random

def factor64(n, seed=0):
    rng = Random(seed)
    factors = []
    todo = [n]
    while todo:
        n = todo.pop()
        if n == 1:
            continue
        if is_prime64(n):
            factors.append(n)
            continue
        if n % 2 == 0:
            d = 2
        else:
            d = n
            while d == n:
                x = y = rng.randrange(n)
                c = rng.randrange(1,n)
                d = 1
                while d == 1:
                    x = (x*x+c) % n
                    y = (y*y+c) % n
                    y = (y*y+c) % n
                    d = gcd(x-y,n)
        todo.extend((d,n//d))
    return sorted(factors)
```

## 考え方

p が n の素因数なら x←x²+c mod n の列を mod p に落としても同じ更新になる。異なる時点の値が mod p で一致すると差と n の GCD に p が現れる。n 自身しか得られない試行は初期値を変える。

### 例題

```python
assert factor64(1000000007*1000000009) == [1000000007,1000000009]
assert factor64(72) == [2,2,2,3,3]
```

[分野の目次](README.md) · [全体の目次](../README.md)
