# イベント処理・スイープライン / Sweep Line

**4/5** · 座標のイベントだけを O(N log N) で走査し、区間の重なりや被覆長を求める。

## 使い方

coverage(intervals) は半開区間 (l,r) の (和集合の長さ,最大重複数)。l≤r。

## コード

```python
from collections import defaultdict

def coverage(intervals):
    events = defaultdict(int)
    for l, r in intervals:
        events[l] += 1
        events[r] -= 1
    length = active = peak = 0
    prev = 0
    for x, delta in sorted(events.items()):
        if active:
            length += x - prev
        active += delta
        peak = max(peak, active)
        prev = x
    return length, peak
```

## 考え方

同じ位置の開始・終了はまとめる。イベントの間は重複数が一定なので、座標の最大値に依存しない。二次元では一方向を走査し、直交方向を Fenwick 木やセグメント木で管理する。

### 例題

```python
assert coverage([(1,4),(3,6),(6,10)]) == (9,2)
```

[分野の目次](README.md) · [全体の目次](../README.md)
