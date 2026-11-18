# 最小除外値・動的 MEX / Minimum Excluded Value / MEX

**4/5** · 一点置換と最小の未出非負整数の照会を合わせて Q 回を O(N+Q log(N+1)) で処理する。

## 使い方

DynamicMex(a) が列のコピーを持つ。set(i,x) で置換し、mex() で最小の未出非負整数。

## コード

```python
from heapq import heapify, heappop, heappush

class DynamicMex:
    def __init__(self, a):
        self.a = list(a)
        n = len(self.a)
        self.freq = [0]*(n+1)
        for x in self.a:
            if 0 <= x <= n:
                self.freq[x] += 1
        self.missing = [x for x,c in enumerate(self.freq) if c == 0]
        heapify(self.missing)
        self.queued = bytearray(c == 0 for c in self.freq)

    def set(self, i, x):
        old = self.a[i]
        if old == x:
            return
        self.a[i] = x
        freq = self.freq
        if 0 <= old < len(freq):
            freq[old] -= 1
            if freq[old] == 0 and not self.queued[old]:
                heappush(self.missing,old)
                self.queued[old] = 1
        if 0 <= x < len(freq):
            freq[x] += 1

    def mex(self):
        heap = self.missing
        while self.freq[heap[0]]:
            self.queued[heappop(heap)] = 0
        return heap[0]
```

## 考え方

N 個の要素では 0〜N のどれかが必ず欠ける。度数が 0 になった値をヒープに入れ、再登場した候補は先頭に来てから捨てる。初期候補と各更新による候補はそれぞれ高々一度取り除かれる。

### 例題

```python
m = DynamicMex([0,2,2,9])
assert m.mex() == 1
m.set(3,1)
assert m.mex() == 3
m.set(0,-1)
assert m.mex() == 0
```

[分野の目次](README.md) · [全体の目次](../README.md)
