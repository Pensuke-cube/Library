# 長方形の和集合面積 / Area of a Union of Rectangles

**3/5** · 軸平行な長方形 N 個の和集合の面積を O(N log N) で求める。

## 使い方

`rect_union_area(rects)` に軸平行な長方形を `(x1, y1, x2, y2)` の列で渡す。`x1 <= x2` と `y1 <= y2` を満たし、幅か高さが 0 のものは無視する。重なる部分を一度だけ数えた面積を返す。長方形がなければ 0。

## コード

```python
def rect_union_area(rects):
    rects = [(x1,y1,x2,y2) for x1,y1,x2,y2 in rects if x1<x2 and y1<y2]
    if not rects:
        return 0
    ys = sorted({y for _,y1,_,y2 in rects for y in (y1,y2)})
    rank = {y:i for i,y in enumerate(ys)}
    events = []
    for x1,y1,x2,y2 in rects:
        l,r = rank[y1],rank[y2]
        events.extend(((x1,l,r,1),(x2,l,r,-1)))
    count = [0]*(4*len(ys))
    covered = [0]*len(count)

    def update(i,l,r,a,b,delta):
        if a <= l and r <= b:
            count[i] += delta
        else:
            m = (l+r)//2
            if a < m:
                update(2*i,l,m,a,b,delta)
            if m < b:
                update(2*i+1,m,r,a,b,delta)
        if count[i] > 0:
            covered[i] = ys[r]-ys[l]
        elif r-l == 1:
            covered[i] = 0
        else:
            covered[i] = covered[2*i]+covered[2*i+1]

    area = 0
    prev = min(event[0] for event in events)
    for x,l,r,delta in sorted(events):
        area += (x-prev)*covered[1]
        update(1,0,len(ys)-1,l,r,delta)
        prev = x
    return area
```

## 考え方

x の開始・終了位置を順に処理する。次のイベントまで被覆長は変わらないため、幅×被覆長を足す。y は座標圧縮し、ノード全域が一つでも覆われていれば実座標の長さを採用する。

### 例題

```python
assert rect_union_area([(0,0,3,2),(2,1,5,3),(9,4,9,8)]) == 11
```

[分野の目次](README.md) · [全体の目次](../README.md)
