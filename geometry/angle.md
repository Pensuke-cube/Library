# 偏角順ソート / Polar Angle Sorting

**3/5** · 原点以外の整数ベクトルを偏角順に O(N log N) で並べる。

## 使い方

`sort_by_angle(points)` に原点からの整数ベクトル `(x, y)` の列を渡す。`(0, 0)` は除く。正の x 軸を起点に反時計回りの順に並べた新しいリストを返す。同じ方向のベクトルは入力順。

## コード

```python
from functools import cmp_to_key

def sort_by_angle(points):
    def half(p):
        x, y = p
        return y < 0 or (y == 0 and x < 0)

    def compare(a, b):
        ha, hb = half(a), half(b)
        if ha != hb:
            return 1 if ha else -1
        z = a[0]*b[1] - a[1]*b[0]
        return (z < 0) - (z > 0)

    return sorted(points, key=cmp_to_key(compare))
```

## 考え方

全周を二つの半平面に分けると、各半平面の角度差は π 未満になり外積で順序が分かる。角度そのものが必要なら atan2(y,x) を使う。

### 例題

```python
assert sort_by_angle([(0,-1),(-1,0),(0,1),(1,0)]) == [(1,0),(0,1),(-1,0),(0,-1)]
```

[分野の目次](README.md) · [全体の目次](../README.md)
