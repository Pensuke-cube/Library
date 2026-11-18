# 優先度付きキュー・遅延削除 / Priority Queue and Lazy Deletion

**5/5** · 最小値を O(1) で参照し、追加・取り出しを O(log N) で行う。

## 使い方

heapify(a) でリストを O(N) でヒープ化する。最大値を取りたい整数は符号を反転して入れる。

## コード

```python
from heapq import heapify, heappop, heappush
```

## 考え方

(a,b) を入れると a、同値なら b で比較する。任意削除や優先度変更は有効な値を別に保存し、ヒープの先頭の古い候補を捨てる。ヒープは古い候補の分だけ大きくなる。

### 例題

```python
priority = [3, 2]
heap = [(3, 0), (2, 1)]
heapify(heap)
priority[1] = 5
heappush(heap, (5, 1))
while heap[0][0] != priority[heap[0][1]]:
    heappop(heap)
assert heap[0] == (3, 0)
```

[分野の目次](README.md) · [全体の目次](../README.md)
