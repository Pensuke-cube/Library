# 最長増加部分列 / Longest Increasing Subsequence

**5/5** · 狭義増加部分列の最大長を O(N log N) で求める。

## 使い方

`a` に数値など順序比較できる値の列を渡す。元の順を保ちつつ、同値を含まない狭義増加の部分列を求める。

- `lis_length(a)` は最大長。`lis_indices(a)` はその長さを達成する 0 始まりの添字列。
- 元の値の列が必要なら `[a[i] for i in lis_indices(a)]`。同値を許す非減少列ではコード中の `bisect_left` を `bisect_right` に替える。

## コード

```python
from bisect import bisect_left

def lis_length(a):
    tails = []
    for x in a:
        i = bisect_left(tails, x)
        if i == len(tails):
            tails.append(x)
        else:
            tails[i] = x
    return len(tails)

def lis_indices(a):
    tails, indices = [], []
    prev = [-1] * len(a)
    for i, x in enumerate(a):
        pos = bisect_left(tails, x)
        if pos:
            prev[i] = indices[pos-1]
        if pos == len(tails):
            tails.append(x)
            indices.append(i)
        else:
            tails[pos], indices[pos] = x, i
    result = []
    i = indices[-1] if indices else -1
    while i >= 0:
        result.append(i)
        i = prev[i]
    return result[::-1]
```

## 考え方

各長さの列の末尾を最小に保つと続きが作りやすい。tails 自体は部分列とは限らない。復元するときは更新した元の添字と一つ短い列の末尾への参照を保存する。

### 例題

```python
assert lis_length([3,1,2,2,5,4]) == 3
a = [3,1,2,2,5,4]
assert [a[i] for i in lis_indices(a)] == [1,2,4]
```

[分野の目次](README.md) · [全体の目次](../README.md)
