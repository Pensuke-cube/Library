# ビット並列 LCS / Bit-Parallel LCS

**3/5** · 最長共通部分列長を各文字につき巨大整数演算数回で求める。

## 使い方

`lcs_bit(a, b)` に文字列や整数リストなど、要素がハッシュ可能な二つの列を渡す。順序を保って両方から取り出せる共通列の最大長を返す。取り出す位置は連続していなくてよい。空の列があれば 0。

## コード

```python
def lcs_bit(a, b):
    if len(a) < len(b):
        a, b = b, a
    masks = {}
    for i, c in enumerate(b):
        masks[c] = masks.get(c, 0) | (1 << i)
    row = 0
    for c in a:
        x = row | masks.get(c, 0)
        row = x & ~(x - ((row << 1) | 1))
    return row.bit_count()
```

## 考え方

DP の一行は隣り合う列で 0 または 1 だけ増える。増加位置をビットで持つ。各増加位置の次に現れる候補を、減算の借りでまとめて選ぶ。反復部は O(N⌈M/w⌉) の目安。マスク表は文字種数とビット長に依存する。

### 例題

```python
assert lcs_bit("competition", "edition") == 6
```

[分野の目次](README.md) · [全体の目次](../README.md)
