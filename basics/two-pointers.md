# しゃくとり法 / Two Pointers / Sliding Window

**5/5** · 両端が単調に進む区間条件を走査する。追加・削除が O(1) なら全体 O(N)。

## 使い方

count_at_most(a,k) は和が k 以下の空でない区間を数える。a は非負整数。

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
