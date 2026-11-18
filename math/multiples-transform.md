# 約数・倍数ゼータ変換とメビウス反転 / Divisor and Multiple Zeta / Möbius Transforms

**3/5** · 1〜N の約数和・倍数和を O(N log log N) で求め、逆変換も同じ時間。

## 使い方

[篩](primes.md)を先に置く。multiple_transform(a,inverse=False) は a[1:] を倍数和に、divisor_transform(a,inverse=False) は約数和に置換する。逆変換は inverse=True。a[0] は使わない。

## コード

```python
def multiple_transform(a, inverse=False):
    n = len(a)-1
    for p, prime in enumerate(sieve(n)):
        if not prime:
            continue
        if inverse:
            for i in range(1,n//p+1):
                a[i] -= a[i*p]
        else:
            for i in range(n//p,0,-1):
                a[i] += a[i*p]

def divisor_transform(a, inverse=False):
    n = len(a)-1
    for p, prime in enumerate(sieve(n)):
        if not prime:
            continue
        if inverse:
            for i in range(n//p,0,-1):
                a[i*p] -= a[i]
        else:
            for i in range(1,n//p+1):
                a[i*p] += a[i]
```

## 考え方

各素数 p について p の冪でつながる添字を一列とみなし、後ろから累積する。逆変換は前から差を取る。GCD が k の組数は、k の倍数だけの組数を作った後に逆変換すれば求まる。

### 例題

```python
a = [0,1,2,3,4,5,6]
multiple_transform(a)
assert a[1:] == [21,12,9,4,5,6]
multiple_transform(a, inverse=True)
assert a == [0,1,2,3,4,5,6]
divisor_transform(a)
assert a[1:] == [1,3,4,7,6,12]
divisor_transform(a, inverse=True)
assert a == [0,1,2,3,4,5,6]
```

[分野の目次](README.md) · [全体の目次](../README.md)
