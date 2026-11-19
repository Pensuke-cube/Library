# 剰余・繰り返し二乗法・逆元 / Modular Arithmetic, Binary Exponentiation and Inverse

**5/5** · 巨大な冪の剰余を O(log K) 回の乗算で求める。逆元は互いに素なとき存在。

## 使い方

- `pow(a, k, m)` は整数 `a` の `k` 乗を正整数 `m` で割った余り。通常のべき乗では `k >= 0`。
- `pow(a, -1, m)` は `m > 1` で `a` と `m` が互いに素のときの逆元。掛けると余りが 1 になる。
- `mod_div(a, b, mod)` は `a` に `b` の逆元を掛けた余り。`mod > 1` で `b` と `mod` が互いに素であること。

## コード

```python
def mod_div(a, b, mod):
    return a * pow(b, -1, mod) % mod
```

## 考え方

加算・減算・乗算では途中で剰余を取れる。除算は逆元との乗算に直す。法が素数なら 0 以外は全て逆元を持ち、Fermat の小定理から pow(b,mod-2,mod) でも得られる。

繰り返し計算では値を Python の整数で持ち、式の最後に % mod を付ける。法が同じなら、各値を剰余クラスのオブジェクトに包む費用を省ける。

### 例題

```python
assert pow(3, 10, 7) == 4 and mod_div(3,2,7) == 5
# 法 7 で x を 3x+2 に 3 回更新する。
x = 1
for _ in range(3):
    x = (3*x + 2) % 7
assert x == 4
```

[分野の目次](README.md) · [全体の目次](../README.md)
