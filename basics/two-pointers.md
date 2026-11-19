# しゃくとり法 / Two Pointers / Sliding Window

**5/5** · 両端が単調に進む区間条件を走査する。追加・削除が O(1) なら全体 O(N)。

## 使い方

`count_at_most(a, k)` に非負整数の列 `a` と区間和の上限 `k` を渡す。`a[l:r]` が空でなく、和が `k` 以下になる `(l, r)` の組数を返す。同じ内容でも位置が異なれば別の区間として数える。

## コード

```python
def count_at_most(a, k):
    if k < 0:
        return 0
    left = total = answer = 0
    for right, x in enumerate(a):
        total += x
        while total > k:
            total -= a[left]
            left += 1
        answer += right - left + 1
    return answer
```

## 考え方

右端を伸ばして条件を破れば左端を進める。各右端について有効な左端が連続することが必要。負の値がある区間和ではこの単調性が崩れる。

### 例題

```python
# 和が 3 以下の区間は [1], [2], [3], [1,2]。
assert count_at_most([1, 2, 3], 3) == 4
```

[分野の目次](README.md) · [全体の目次](../README.md)
