# 単調キュー・単調スタック / Monotonic Queue and Stack

**4/5** · 全固定幅区間の最小値や各要素の直前の小さい要素を O(N) で求める。

## 使い方

window_min(a,k) は幅 k の区間最小値。previous_smaller(a) は左の最も近い真に小さい要素の添字（なければ -1）。

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
