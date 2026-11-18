# 凸包 / Convex Hull / Monotone Chain

**3/5** · 点群を囲む最小の凸多角形を O(N log N) で求める。

## 使い方

[外積](orientation.md)を先に置く。convex_hull(points) は反時計回りの頂点列。重複や辺の途中の点を除く。

## コード

```python
def convex_hull(points):
    points = sorted(set(points))
    if len(points) <= 1:
        return points

    def half(order):
        chain = []
        for p in order:
            while len(chain) >= 2 and cross(chain[-2],chain[-1],p) <= 0:
                chain.pop()
            chain.append(p)
        return chain

    return half(points)[:-1] + half(reversed(points))[:-1]
```

## 考え方

x 座標順に半分ずつ凸包を作る。新しい点で右折するなら直前の点は外周に不要。二つの鎖を結ぶと外周になる。全点が一直線なら両端だけ返る。

### 例題

```python
assert convex_hull([(0,0),(2,0),(2,2),(0,2),(1,1)]) == [(0,0),(2,0),(2,2),(0,2)]
```

[分野の目次](README.md) · [全体の目次](../README.md)
