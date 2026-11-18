# 行列積・行列累乗 / Matrix Multiplication and Exponentiation

**4/5** · 線形な状態遷移の K 回先を O(D³ log K) で求める。

## 使い方

mat_pow(a,k,mod) は D×D の正方行列の k 乗。k≥0、mod>0。

## コード

```python
def mat_mul(a, b, mod):
    cols = list(zip(*b))
    return [[sum(x*y for x,y in zip(row,col)) % mod for col in cols] for row in a]

def mat_pow(a, k, mod):
    n = len(a)
    result = [[int(i==j) % mod for j in range(n)] for i in range(n)]
    while k:
        if k & 1:
            result = mat_mul(result, a, mod)
        k >>= 1
        if k:
            a = mat_mul(a, a, mod)
    return result
```

## 考え方

状態ベクトルを更新する遷移を行列 A とすると K 回後は A^K を掛ける。隣接行列の累乗では要素 (i,j) が長さ K の歩道数になる。

### 例題

```python
assert mat_pow([[1,1],[1,0]], 5, 10**9+7)[0][1] == 5
```

[分野の目次](README.md) · [全体の目次](../README.md)
