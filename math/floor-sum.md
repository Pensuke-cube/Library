# 床関数の和 / Floor Sum

**3/5** · Σ floor((ai+b)/m) を m の対数回の反復で求める。

## 使い方

floor_sum(n,m,a,b) の範囲は 0≤i<n。n≥0、m>0、a,b は負でもよい。

## コード

```python
def floor_sum(n, m, a, b):
    ans = 0
    while True:
        aq, a = divmod(a, m)
        bq, b = divmod(b, m)
        ans += aq*n*(n-1)//2 + bq*n
        ymax = a*n + b
        if ymax < m:
            return ans
        n, b = divmod(ymax, m)
        a, m = m, a
```

## 考え方

a,b の m の倍数分は等差数列と定数の和。残りは直線の下の格子点数で、横・縦の数え方を交換すると法が小さくなる。m→a→m mod a と Euclid と同様に減る。

### 例題

```python
assert floor_sum(10,7,-3,5) == sum((-3*i+5)//7 for i in range(10))
```

[分野の目次](README.md) · [全体の目次](../README.md)
