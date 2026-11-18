# 全探索・順列・組合せ / Enumeration, Permutations and Combinations

**5/5** · 2^N 個の部分集合、N! 個の順列、二項係数個の組合せを列挙する。

## 使い方

permutations(a)、combinations(a, r)、product(*choices) で各候補を順に得る。

## コード

```python
from itertools import combinations, permutations, product

def subsets(a):
    for mask in range(1 << len(a)):
        yield [x for i, x in enumerate(a) if mask >> i & 1]
```

## 考え方

候補を一つ作る費用も数える。二値の独立な選択はビット集合、相互排他的な並びは順列、順序を問わない選択は組合せ。重複する値があっても位置を区別する。

### 例題

```python
assert sorted(sum(s) for s in subsets([2, 3])) == [0, 2, 3, 5]
assert list(combinations([1, 2, 3], 2)) == [(1, 2), (1, 3), (2, 3)]
```

[分野の目次](README.md) · [全体の目次](../README.md)
