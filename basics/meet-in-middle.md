# 半分全列挙 / Meet in the Middle

**4/5** · 部分集合問題を二分し、O(N·2^(N/2)) 時間と O(2^(N/2)) 空間で合成する。

## 使い方

`subset_sum_leq(a, limit)` に整数の列 `a` と和の上限 `limit` を渡す。各位置を高々一度選べるとき、上限以下の最大の和を返す。負の要素も可。空集合の和 0 も候補で、条件を満たす選び方がなければ `None`。

## コード

```python
from bisect import bisect_right

def subset_sum_leq(a, limit):
    def sums(values):
        result = [0]
        for x in values:
            result += [s + x for s in result]
        return result

    mid = len(a) // 2
    right = sorted(sums(a[mid:]))
    answer = None
    for x in sums(a[:mid]):
        j = bisect_right(right, limit - x)
        if j:
            s = x + right[j - 1]
            if answer is None or s > answer:
                answer = s
    return answer
```

## 考え方

各部分集合は左半分と右半分に分かれる。左の和 x が決まれば、右から limit-x 以下の最大値を取る。個数を数えるなら二分探索の添字を加算する。

### 例題

```python
assert subset_sum_leq([3, 8, 9, 12], 20) == 20
assert subset_sum_leq([-3, 2], -4) is None
```

[分野の目次](README.md) · [全体の目次](../README.md)
