# 2-opt・巡回路の差分評価 / 2-opt and Incremental Scoring

**5/5** · 対称な巡回路の区間反転を O(1) で評価する。採用時の反転は区間長に比例。

## 使い方

two_opt_delta(tour,l,r,dist) は [l,r) を反転したときの距離増分。0≤l<r≤len(tour)。dist は対称。

## コード

```python
def two_opt_delta(tour, l, r, dist):
    if l == 0 and r == len(tour):
        return 0
    a, b = tour[l-1], tour[l]
    c, d = tour[r-1], tour[r % len(tour)]
    return dist[a][c] + dist[b][d] - dist[a][b] - dist[c][d]
```

## 考え方

区間内部は各辺の方向だけ反転し、対称距離では合計が変わらない。変化する境界 2 辺だけ比較する。非対称距離では内部反転分も必要。

### 例題

```python
p = [0,1,3,2]
d = [[abs(i-j) for j in range(4)] for i in range(4)]
delta = two_opt_delta(p,1,3,d)
score = lambda a: sum(d[a[i-1]][x] for i,x in enumerate(a))
q = p[:1] + p[1:3][::-1] + p[3:]
assert delta == score(q)-score(p)
```

[分野の目次](README.md) · [全体の目次](../README.md)
