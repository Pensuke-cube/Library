# ガウス消去・線形基底 / Gaussian Elimination and XOR Basis

**3/5** · GF(2) の線形独立性や XOR で表せる値を O(NB) 回の整数演算で求める。

## 使い方

`XorBasis(bits)` に扱うビット数を渡す。各値 `x` は `0 <= x < 2**bits` の整数。

- `add(x)` は既存の値の XOR で作れないときだけ基底に追加して `True` を返す。`rank` は基底の個数。
- `contains(x)` は登録済みの値の一部を XOR して `x` を作れるか。何も使わない場合の 0 も含む。
- `reduce(x)` は上位ビットから基底で消した結果。0 なら `x` を作れる。

## コード

```python
class XorBasis:
    def __init__(self, bits):
        self.basis = [0] * bits
        self.rank = 0

    def reduce(self, x):
        while x:
            i = x.bit_length()-1
            if not self.basis[i]:
                break
            x ^= self.basis[i]
        return x

    def add(self, x):
        x = self.reduce(x)
        if not x:
            return False
        self.basis[x.bit_length()-1] = x
        self.rank += 1
        return True

    def contains(self, x):
        return self.reduce(x) == 0
```

## 考え方

最上位ビットをピボットにし、既存の基底で消してから追加する。rank 個の独立な基底があれば 2^rank 種の XOR が作れる。一般の体では XOR を行の加減算に替え、ピボット係数で割る。

### 例題

```python
b = XorBasis(4)
assert b.add(6) and b.add(3) and not b.add(5)
assert b.contains(5) and not b.contains(8) and b.rank == 2
```

[分野の目次](README.md) · [全体の目次](../README.md)
