# 累積和で DP の遷移を高速化 / Prefix-Sum DP Optimization

**4/5** · 直前の状態の連続範囲の和を O(1) で取り、配分数を O(NK) で求める。

## 使い方

bounded_distributions(caps,k,mod) は子 i に 0〜caps[i] 個配り、合計 k 個にする方法数。

## コード

```python
def bounded_distributions(caps, k, mod):
    dp = [1] + [0] * k
    for c in caps:
        nxt = [0] * (k+1)
        window = 0
        for j in range(k+1):
            window += dp[j]
            if j > c:
                window -= dp[j-c-1]
            nxt[j] = window % mod
        dp = nxt
    return dp[k] % mod
```

## 考え方

j 個を配る遷移は、直前の dp[max(0,j-c):j+1] の和。j を一つ進めると右端が入り、幅の外に出た左端が抜ける。一行分の累積和を別に作って引いてもよい。

### 例題

```python
assert bounded_distributions([1,2,3], 4, 998244353) == 5
```

[分野の目次](README.md) · [全体の目次](../README.md)
