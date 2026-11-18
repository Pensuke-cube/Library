# 畳み込み・整数パッキング / Convolution and Integer Packing

**4/5** · 積の係数列を整数乗算一回で求める。計算量はパック後の整数乗算に依存。

## 使い方

convolution(a,b,mod) は整数列の畳み込みを mod>0 で返す。空配列なら []。

## コード

```python
def convolution(a, b, mod=998244353):
    if not a or not b:
        return []
    a, b = [x % mod for x in a], [x % mod for x in b]
    bound = min(len(a),len(b))*max(a)*max(b)
    width = max(1, (bound.bit_length()+7)//8)
    def pack(values):
        data = b"".join(x.to_bytes(width, "little") for x in values)
        return int.from_bytes(data, "little")
    n = len(a)+len(b)-1
    data = (pack(a)*pack(b)).to_bytes(n*width, "little")
    return [int.from_bytes(data[i:i+width], "little") % mod for i in range(0,len(data),width)]
```

## 考え方

係数を固定長の桁に置くと整数積の各桁に係数の積和が現れる。桁の基数は最大の積和より大きくし、桁上がりを防ぐ。法が 998244353 なら [NTT](ntt.md) を優先する。

### 例題

```python
assert convolution([1,2,3], [4,5]) == [4,13,22,15]
assert convolution([-1,2], [4], 7) == [3,1]
```

[分野の目次](README.md) · [全体の目次](../README.md)
