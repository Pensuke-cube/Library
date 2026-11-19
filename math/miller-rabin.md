# ミラー–ラビン素数判定 / Miller–Rabin Primality Test

**3/5** · 64 ビット非負整数の素数判定を少数回の冪剰余で行う。

## 使い方

`is_prime64(n)` に `0 <= n < 2**64` の整数を渡す。素数なら `True`、合成数または 0・1 なら `False`。この範囲では固定の基底で判定できる。

## コード

```python
def is_prime64(n):
    if n < 2 or n % 2 == 0:
        return n == 2
    d = n - 1
    s = (d & -d).bit_length() - 1
    d >>= s
    for a in (2, 325, 9375, 28178, 450775, 9780504, 1795265022):
        if a % n == 0:
            continue
        x = pow(a, d, n)
        if x in (1, n-1):
            continue
        for _ in range(s-1):
            x = x*x % n
            if x == n-1:
                break
        else:
            return False
    return True
```

## 考え方

n-1 を 2^s·d と分ける。素数なら a^d=1 か、二乗列のどこかで -1 を通る。記載の基底集合で 2^64 未満は決定的。各基底は O(log n) 回の剰余乗算。

### 例題

```python
assert is_prime64(2**61-1)
assert not is_prime64(341550071728321)
```

[分野の目次](README.md) · [全体の目次](../README.md)
