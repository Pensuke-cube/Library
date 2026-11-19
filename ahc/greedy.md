# 初期解・貪欲構築 / Greedy Construction

**5/5** · 実行可能な初期解を作る。最近傍で巡回順を作る例は O(N²)。

## 使い方

`nearest_tour(dist, start=0)` に空でない距離行列 `dist` を渡す。`dist[i][j]` は点 `i` から点 `j` への距離、`start` は出発点の番号。各点を一度ずつ訪れる番号のリストを返す。末尾に出発点は重ねず、巡回距離を出すときに末尾から先頭への辺を足す。

## コード

```python
def nearest_tour(dist, start=0):
    remaining = set(range(len(dist)))
    remaining.remove(start)
    tour = [start]
    while remaining:
        row = dist[tour[-1]]
        nxt = min(remaining, key=lambda v: (row[v], v))
        remaining.remove(nxt)
        tour.append(nxt)
    return tour
```

## 考え方

まず出力条件を満たす構築を作る。局所の評価が同じなら頂点番号などで順序を固定すると再現しやすい。複数の始点や順序で作って、最も良い完成解を残せる。

### 例題

```python
d = [[0,1,4], [1,0,2], [4,2,0]]
assert nearest_tour(d) == [0,1,2]
```

[分野の目次](README.md) · [全体の目次](../README.md)
