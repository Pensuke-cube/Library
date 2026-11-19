# 数論変換・高速畳み込み / Number-Theoretic Transform / NTT

**3/5** · 998244353 を法とする畳み込みを O(L log L) で求める。

## 使い方

`convolution_ntt(a, b)` に低い次数から係数を並べた二つの整数列を渡す。積の係数を同じ順で、`998244353` で割った余りとして返す。どちらかが空なら `[]`。空でなければ結果長 `len(a)+len(b)-1` が `2**23` 以下であること。

## コード

```python
def convolution_ntt(a, b):
    if not a or not b:
        return []
    mod = 998244353
    need = len(a)+len(b)-1
    n = 1 << (need-1).bit_length()
    if n > 1 << 23:
        raise ValueError("NTT length exceeds 2**23")

    def transform(a, inverse):
        j = 0
        for i in range(1,n):
            bit = n >> 1
            while j & bit:
                j ^= bit
                bit >>= 1
            j ^= bit
            if i < j:
                a[i], a[j] = a[j], a[i]
        width = 2
        while width <= n:
            root = pow(3, (mod-1)//width, mod)
            if inverse:
                root = pow(root, -1, mod)
            half = width//2
            for start in range(0,n,width):
                w = 1
                for i in range(start,start+half):
                    u, v = a[i], a[i+half]*w % mod
                    a[i], a[i+half] = (u+v)%mod, (u-v)%mod
                    w = w*root % mod
            width *= 2
        if inverse:
            inv = pow(n,-1,mod)
            for i in range(n):
                a[i] = a[i]*inv % mod

    x = [v % mod for v in a] + [0]*(n-len(a))
    y = [v % mod for v in b] + [0]*(n-len(b))
    transform(x, False)
    transform(y, False)
    for i in range(n):
        x[i] = x[i]*y[i] % mod
    transform(x, True)
    return x[:need]
```

## 考え方

多項式を L 個の異なる L 乗根で評価し、対応する値を掛けて逆変換する。法が 998244353 のとき 3 は原始根で、法−1 が 2^23 で割り切れる。L より長い積は巻き戻るので結果長を確保する。

### 例題

```python
assert convolution_ntt([1,2,3], [4,5]) == [4,13,22,15]
assert convolution_ntt([-1], [1]) == [998244352]
```

[分野の目次](README.md) · [全体の目次](../README.md)
