# 包除原理・倍数の数え上げ / Inclusion–Exclusion Principle

**4/5** · 重複する条件の和集合の大きさを O(2^K) 回の共通部分計算で求める。

## 使い方

count_multiples(n,values) は 1〜n で正整数 values のいずれかの倍数である数の個数。

## コード

```python
from math import lcm

def count_multiples(n, values):
    def dfs(i, base, sign):
        total = 0
        for j in range(i,len(values)):
            common = lcm(base, values[j])
            if common <= n:
                total += sign*(n//common) + dfs(j+1, common, -sign)
        return total
    return dfs(0, 1, 1)
```

## 考え方

二条件とも満たす数は二重に足されるので引く。三条件以上も共通部分のサイズに応じて交互に足し引きする。共通倍数は最小公倍数の倍数で、n を超えた枝は寄与しない。

### 例題

```python
assert count_multiples(12, [2,3]) == 8
```

[分野の目次](README.md) · [全体の目次](../README.md)
