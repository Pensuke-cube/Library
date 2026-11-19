# 単調キュー・単調スタック / Monotonic Queue and Stack

**4/5** · 全固定幅区間の最小値や各要素の直前の小さい要素を O(N) で求める。

## 使い方

`a` に順序比較できる値の列を渡す。

- `window_min(a, k)` は幅 `k`（`1 <= k <= len(a)`）の各連続区間の最小値。`result[l]` は `a[l:l+k]` の最小値。
- `previous_smaller(a)` の `result[i]` は、`i` より左で `a[i]` より真に小さい要素のうち最も近い添字。なければ `-1`。

## コード

```python
from collections import deque

def window_min(a, k):
    q = deque()
    answer = []
    for i, x in enumerate(a):
        while q and q[0] <= i - k:
            q.popleft()
        while q and a[q[-1]] >= x:
            q.pop()
        q.append(i)
        if i + 1 >= k:
            answer.append(a[q[0]])
    return answer

def previous_smaller(a):
    stack = []
    answer = []
    for i, x in enumerate(a):
        while stack and a[stack[-1]] >= x:
            stack.pop()
        answer.append(stack[-1] if stack else -1)
        stack.append(i)
    return answer
```

## 考え方

新しい値が古い候補以下なら、古い候補は以後の最小値に不要。スタックで左右の境界を求めると、各棒を最小高とする最大幅が分かる。

### 例題

```python
assert window_min([4, 1, 3, 2], 2) == [1, 1, 2]
assert previous_smaller([4, 1, 3, 2]) == [-1, -1, 1, 1]
```

[分野の目次](README.md) · [全体の目次](../README.md)
