# 部分和のビット集合 DP / Subset Sum Bitset DP

**4/5** · 非負整数の部分和の到達可否をシフトと OR で一括更新する。

## 使い方

subset_sum(a,target) は和が target になる部分集合の有無。target≥0、a の値は非負。

## コード

```python
def subset_sum(a, target):
    bits = 1
    limit = (1 << (target + 1)) - 1
    for x in a:
        if x <= target:
            bits = (bits | (bits << x)) & limit
    return bool(bits >> target & 1)
```

## 考え方

ビット s が立つことは和 s を作れることを表す。x を選ぶなら x ビット分左にずらす。一回の更新は巨大整数を扱うので整数の内部桁数に比例する。

### 例題

```python
assert subset_sum([2,5,8], 10)
assert not subset_sum([2,5,8], 4)
```

[分野の目次](README.md) · [全体の目次](../README.md)
