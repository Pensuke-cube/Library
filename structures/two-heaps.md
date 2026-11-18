# 中央値・上下二つのヒープ / Running Median with Two Heaps

**4/5** · 数を O(log N) で追加し、下側中央値を O(1) で求める。

## 使い方

RunningMedian().add(x) で整数を追加。median() は中央二値のうち小さい方で、空なら None。

## コード

```python
from heapq import heappush, heappop

class RunningMedian:
    def __init__(self):
        self.low = []
        self.high = []

    def add(self, x):
        low, high = self.low, self.high
        if not low or x <= -low[0]:
            heappush(low,-x)
        else:
            heappush(high,x)
        if len(low) < len(high):
            heappush(low,-heappop(high))
        elif len(low) > len(high)+1:
            heappush(high,-heappop(low))

    def median(self):
        return -self.low[0] if self.low else None
```

## 考え方

小さい半分は最大ヒープ、大きい半分は最小ヒープに置く。両側のサイズ差を 0 または 1 に維持する。両側の和も更新すると、中央値からの絶対偏差の総和を O(1) で求められる。

### 例題

```python
m = RunningMedian()
answer = []
for x in [5,1,4,0]:
    m.add(x)
    answer.append(m.median())
assert answer == [5,1,4,1]
```

[分野の目次](README.md) · [全体の目次](../README.md)
