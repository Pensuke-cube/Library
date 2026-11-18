# 剰余・繰り返し二乗法・逆元 / Modular Arithmetic, Binary Exponentiation and Inverse

**5/5** · 巨大な冪の剰余を O(log K) 回の乗算で求める。逆元は互いに素なとき存在。

## 使い方

pow(a,k,m) で a^k mod m。pow(a,-1,m) で逆元（m>1、gcd(a,m)=1）。

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
