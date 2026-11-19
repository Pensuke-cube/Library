# ビット演算・部分マスク列挙 / Bit Operations and Submasks

**4/5** · 集合を整数で表し、立っているビットや 2^k 個の部分集合を列挙する。

## 使い方

非負整数 `mask` の i ビット目が 1 なら要素 `i` を含む。例えば `0b1010` は要素 `1` と `3`。

- `bit_indices(mask)` は立っているビットの位置を昇順に列挙する。
- `submasks(mask)` は、そのビットの一部だけを立てた整数を降順に列挙する。元の `mask` と `0` を含む。

## コード

```python
def submasks(mask):
    sub = mask
    while sub:
        yield sub
        sub = (sub - 1) & mask
    yield 0

def bit_indices(mask):
    while mask:
        low = mask & -mask
        yield low.bit_length() - 1
        mask ^= low
```

## 考え方

和集合は |、積集合は &、対称差は ^、要素数は bit_count()。全マスクの部分マスクを合わせて走査すると各ビットが 3 状態を取るため O(3^N)。

### 例題

```python
assert list(submasks(0b101)) == [5, 4, 1, 0]
assert list(bit_indices(0b1010)) == [1, 3]
```

[分野の目次](README.md) · [全体の目次](../README.md)
