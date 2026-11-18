# 距離・マンハッタン距離 / Distance and Manhattan Distance

**4/5** · 二点距離を O(1)、全点対の最大マンハッタン距離を O(N) で求める。

## 使い方

manhattan_diameter(points) は空でない二次元点列の最大 L1 距離。

## コード

```python
def squared_distance(a, b):
    return (a[0]-b[0])**2 + (a[1]-b[1])**2

def manhattan_diameter(points):
    u, v = zip(*((x+y,x-y) for x,y in points))
    return max(max(u)-min(u), max(v)-min(v))
```

## 考え方

L2 距離の比較は二乗のままでできる。二次元 L1 の |dx|+|dy| は max(|dx+dy|,|dx-dy|) と等しい。変換先の各軸の最大値と最小値だけで最遠点対が分かる。

### 例題

```python
assert squared_distance((0,0),(3,4)) == 25
assert manhattan_diameter([(1,2),(4,0),(-1,2)]) == 7
```

[分野の目次](README.md) · [全体の目次](../README.md)
