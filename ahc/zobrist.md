# Zobrist ハッシュ・状態重複除去 / Zobrist Hashing

**4/5** · 局所変更後の状態ハッシュを変更箇所数に比例する時間で更新する。

## 使い方

`zobrist_table(n, k, seed=0)` に状態の要素数 `n` と各要素が取り得る値の種類数 `k` を渡す。値は `0` から `k-1`。同じ `seed` なら同じ表を作る。

`hash_state(a, table)` に長さ `n` の状態列とその表を渡すと整数ハッシュを返す。位置 `i` の値を `old` から `new` に変えるときは `h ^= table[i][old] ^ table[i][new]` で更新する。

## コード

```python
from random import Random

def zobrist_table(n, k, seed=0):
    rng = Random(seed)
    return [[rng.getrandbits(64) for _ in range(k)] for _ in range(n)]

def hash_state(a, table):
    h = 0
    for i, x in enumerate(a):
        h ^= table[i][x]
    return h
```

## 考え方

位置と値の組に独立の乱数を割り当てる。同じ値を XOR すると相殺するので変更前の寄与だけ消せる。衝突を許せない場合はハッシュ一致時に元の状態も比較する。

### 例題

```python
z = zobrist_table(3, 2)
a = [0,1,0]
h = hash_state(a,z)
h ^= z[1][1] ^ z[1][0]
a[1] = 0
assert h == hash_state(a,z)
```

[分野の目次](README.md) · [全体の目次](../README.md)
