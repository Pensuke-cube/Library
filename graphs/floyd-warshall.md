# ワーシャル–フロイド法 / Floyd–Warshall Algorithm

**4/5** · 全頂点対の最短距離を O(V³) 時間・O(V²) 空間で求める。

## 使い方

floyd_warshall(n,edges) の辺は (始点,終点,重み)。有向、負辺可。負閉路は d[i][i]<0 で分かる。

## コード

```python
def floyd_warshall(n, edges):
    inf = float("inf")
    d = [[inf] * n for _ in range(n)]
    for i in range(n):
        d[i][i] = 0
    for a, b, w in edges:
        if w < d[a][b]:
            d[a][b] = w
    for k, dk in enumerate(d):
        for di in d:
            via = di[k]
            if via == inf:
                continue
            for j, tail in enumerate(dk):
                if tail == inf:
                    continue
                nd = via + tail
                if nd < di[j]:
                    di[j] = nd
    return d
```

## 考え方

最外ループの k は経由してよい頂点の追加。負閉路のある入力で、そこを経由できるペアの距離は下限がない。戻り値で該当ペアを判定するには到達性も確認する。

### 例題

```python
d = floyd_warshall(3, [(0,1,3),(1,2,-2),(0,2,6)])
assert d[0][2] == 1 and d[2][0] == float("inf")
```

[分野の目次](README.md) · [全体の目次](../README.md)
