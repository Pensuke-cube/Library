# 外積・線分交差 / Cross Product and Segment Intersection

**4/5** · 整数座標で回転方向や端点を含む線分交差を O(1) 回の演算で判定する。

## 使い方

点は二次元の座標 `(x, y)` で渡す。

- `cross(a, b, c)` は A→B と A→C の外積。正なら A→B から見て C は左、負なら右、0 なら同一直線上（A=B のときも 0）。
- `intersects(a, b, c, d)` は線分 AB と CD が一点でも共有するなら `True`。端点も含む。同じ点を両端にしてもよい。

## コード

```python
def cross(a, b, c):
    return (b[0]-a[0])*(c[1]-a[1]) - (b[1]-a[1])*(c[0]-a[0])

def intersects(a, b, c, d):
    for i in range(2):
        if max(min(a[i],b[i]), min(c[i],d[i])) > min(max(a[i],b[i]), max(c[i],d[i])):
            return False
    return cross(a,b,c)*cross(a,b,d) <= 0 and cross(c,d,a)*cross(c,d,b) <= 0
```

## 考え方

外積の符号は左・右・同一直線に対応する。互いの線分の端点が反対側か直線上にあれば交差候補。同一直線上で遠く離れた線分は座標範囲で除く。

### 例題

```python
assert intersects((0,0),(2,2),(0,2),(2,0))
assert not intersects((0,0),(1,1),(2,2),(3,3))
```

[分野の目次](README.md) · [全体の目次](../README.md)
