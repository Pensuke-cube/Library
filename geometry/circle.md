# 円の位置関係・距離比較 / Circle Relations

**3/5** · 二円が交わるか、接するか、一方が内側かを O(1) 回の整数演算で判定する。

## 使い方

circle_intersections(a,b) の円は (x,y,r)、r>0。共通点の個数 0〜2 を返す。同一円は None。

## コード

```python
def circle_intersections(a, b):
    x,y,r = a
    u,v,s = b
    d2 = (x-u)**2 + (y-v)**2
    inner, outer = (r-s)**2, (r+s)**2
    if d2 == 0 and r == s:
        return None
    if d2 < inner or outer < d2:
        return 0
    if d2 == inner or d2 == outer:
        return 1
    return 2
```

## 考え方

交差条件は |r-s|≤中心間距離≤r+s。境界なら接する。座標・半径が整数なら両辺を二乗して誤差なく比べられる。円周上の点も中心からの二乗距離と r² の一致で判定できる。

### 例題

```python
assert circle_intersections((0,0,2),(3,0,1)) == 1
assert circle_intersections((0,0,2),(1,0,2)) == 2
assert circle_intersections((0,0,2),(0,0,1)) == 0
```

[分野の目次](README.md) · [全体の目次](../README.md)
