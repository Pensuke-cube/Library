# 多角形の面積 / Polygon Area / Shoelace Formula

**3/5** · 巡回順の頂点から符号付き面積の二倍を O(N) で求める。

## 使い方

`area2(p)` に多角形の頂点 `(x, y)` を辺に沿った順で渡す。末尾に先頭を重ねる必要はない。面積の 2 倍を返し、反時計回りなら正、時計回りなら負。整数座標なら結果も厳密な整数で、通常の面積は `abs(area2(p)) / 2`。

## コード

```python
def area2(p):
    total = 0
    for i, (x,y) in enumerate(p):
        u,v = p[i-1]
        total += u*y - v*x
    return total
```

## 考え方

原点と各辺の作る三角形の符号付き面積を足す。多角形の外側に出た分は逆符号で相殺する。格子多角形の内部格子点は Pick の定理で abs(area2)/2-B/2+1。B は各辺の gcd(|dx|,|dy|) の和。

### 例題

```python
assert area2([(0,0),(3,0),(0,2)]) == 6
```

[分野の目次](README.md) · [全体の目次](../README.md)
