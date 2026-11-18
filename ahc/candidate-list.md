# 候補リスト・近傍の絞り込み / Candidate Lists and Neighborhood Pruning

**4/5** · 各点で評価する近傍を N 個から K 個に絞る。例の前処理は O(N² log(K+1))。

## 使い方

nearest_candidates(dist,k) は各点の近い K 点。自己点を除く。dist[i][j] は点 i から j への距離。

## コード

```python
from heapq import nsmallest

def nearest_candidates(dist, k):
    return [
        nsmallest(k,(j for j in range(len(dist)) if j!=i),key=row.__getitem__)
        for i,row in enumerate(dist)
    ]
```

## 考え方

TSP では新しく張る辺が短い操作から試す。近傍全列挙より一周が軽くなる一方、候補外の改善は見落とす。停滞したら K を増やすか、候補外からも確率的に試す。

### 例題

```python
d = [[0,1,4],[1,0,2],[4,2,0]]
assert nearest_candidates(d,1) == [[1],[0],[1]]
```

[分野の目次](README.md) · [全体の目次](../README.md)
