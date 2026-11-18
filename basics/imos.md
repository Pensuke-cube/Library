# いもす法・二次元いもす法 / Difference Array / Imos Method

**5/5** · Q 回の区間・長方形加算を記録し、全点を O(N+Q) または O(HW+Q) で復元する。

## 使い方

各更新は (l,r,x) または (上,左,下,右,x)。右端・下端は含めない。

## コード

```python
from itertools import accumulate

def imos(n, updates):
    d = [0] * (n + 1)
    for l, r, x in updates:
        d[l] += x
        d[r] -= x
    d.pop()
    return list(accumulate(d))

def imos_2d(h, w, updates):
    d = [[0] * (w + 1) for _ in range(h + 1)]
    for t, l, b, r, x in updates:
        d[t][l] += x
        d[b][l] -= x
        d[t][r] -= x
        d[b][r] += x
    for i in range(h):
        row = list(accumulate(d[i][:w]))
        d[i] = [x + y for x, y in zip(row, d[i-1])] if i else row
    return d[:h]
```

## 考え方

加算の開始と終了だけを記録する。二次元では四隅に符号を付け、横と縦をそれぞれ累積する。更新と質問が交互なら Fenwick 木などを使う。

### 例題

```python
assert imos(4, [(0, 2, 3), (1, 4, 2)]) == [3, 5, 2, 2]
assert imos_2d(2, 2, [(0, 1, 2, 2, 3)]) == [[0, 3], [0, 3]]
```

[分野の目次](README.md) · [全体の目次](../README.md)
