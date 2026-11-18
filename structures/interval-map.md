# 連続区間の管理・区間の併合 / Interval Set and Interval Merging

**4/5** · 半開区間の和集合を重複しない区間の列にまとめる。O(N log N)。

## 使い方

merge_intervals(intervals) は重なる区間や接する区間を併合する。l≤r。空区間は捨てる。

## コード

```python
def merge_intervals(intervals):
    merged = []
    for l,r in sorted(intervals):
        if l == r:
            continue
        if merged and l <= merged[-1][1]:
            l0,r0 = merged[-1]
            merged[-1] = l0,max(r,r0)
        else:
            merged.append((l,r))
    return merged
```

## 考え方

開始位置の昇順で処理すると、新区間と重なる可能性があるのは最後の区間だけ。動的な追加では左端を順序付き集合に置き、開始位置の直前の区間と右側の重なる区間を消してから合体した区間を入れる。

### 例題

```python
assert merge_intervals([(6,7),(0,1),(1,3),(3,3),(2,5)]) == [(0,5),(6,7)]
```

[分野の目次](README.md) · [全体の目次](../README.md)
