# 組合せ・階乗・二項係数 / Combinatorics and Binomial Coefficients

**5/5** · 素数法で階乗を前処理し、二項係数・順列数を O(1) で答える。

## 使い方

Comb(n,mod) は mod が素数で n<mod。comb(n,k) と perm(n,k)。正確な値が必要なら math.comb。

## コード

```python
class Comb:
    def __init__(self, n, mod=998244353):
        self.mod = mod
        self.fact = f = [1] * (n+1)
        self.inv_fact = inv = [1] * (n+1)
        for i in range(1,n+1):
            f[i] = f[i-1]*i % mod
        inv[n] = pow(f[n], -1, mod)
        for i in range(n,0,-1):
            inv[i-1] = inv[i]*i % mod

    def comb(self, n, k):
        if not 0 <= k <= n:
            return 0
        return self.fact[n] * self.inv_fact[k] * self.inv_fact[n-k] % self.mod

    def perm(self, n, k):
        if not 0 <= k <= n:
            return 0
        return self.fact[n] * self.inv_fact[n-k] % self.mod
```

## 考え方

nCk=n!/(k!(n-k)!)。逆階乗は最大の階乗を一度だけ反転して、逆順に掛けて戻す。和 n の非負整数を k 個並べる方法は k≥1 なら (n+k-1)C(k-1)。

### 例題

```python
c = Comb(12)
assert c.comb(6,2) == 15 and c.perm(6,2) == 30
```

[分野の目次](README.md) · [全体の目次](../README.md)
