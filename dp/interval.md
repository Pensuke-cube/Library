# 区間 DP / Interval DP

**4/5** · 区間内の分割や消去を短い区間から解く。全分割を試す例は O(N³)。

## 使い方

`merge_cost(a)` に要素の重さの列 `a` を渡す。各要素を別々の区間として始め、隣り合う二つを合計の重さを払って併合する。一つの区間にするまでの費用の合計が最小になる値を返す。要素が 0 個か 1 個なら 0。

## コード

```python
from itertools import accumulate

def merge_cost(a):
    n = len(a)
    p = list(accumulate(a, initial=0))
    dp = [[0] * (n+1) for _ in range(n+1)]
    for width in range(2, n+1):
        for l in range(n-width+1):
            r = l + width
            dp[l][r] = p[r]-p[l] + min(dp[l][k]+dp[k][r] for k in range(l+1,r))
    return dp[0][n]
```

## 考え方

最後の併合直前は [l,k) と [k,r) の二個。左右を作る費用と最後の併合費用を足す。長さ 0 や 1 の初期値を問題に合わせる。

### 例題

```python
assert merge_cost([10,20,30]) == 90
```

[分野の目次](README.md) · [全体の目次](../README.md)
