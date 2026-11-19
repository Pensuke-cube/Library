# 木 DP / Tree Dynamic Programming

**5/5** · 子から親への集約で木の独立集合などを求める。例は O(N)。

## 使い方

[根付き化](euler-tour.md)のコードを先に置く。`independent_sets(g, mod)` の `g[v]` に頂点 `v` の隣接先を並べる。空でない無向木を使い、頂点番号は 0 始まり、辺は両方向を登録する。`mod` は正整数。

辺で直接つながる二頂点を同時に選ばない頂点集合の個数を、`mod` で割った余りで返す。空集合も含む。

## コード

```python
def independent_sets(g, mod):
    parent, _, order, _, _ = root_tree(g)
    skip, take = [1] * len(g), [1] * len(g)
    for v in reversed(order[1:]):
        p = parent[v]
        skip[p] = skip[p] * (skip[v] + take[v]) % mod
        take[p] = take[p] * skip[v] % mod
    return (skip[0] + take[0]) % mod
```

## 考え方

親を選ぶかどうかで子に課される条件が決まる。親を選ぶなら子を選べず、選ばないなら両方可能。異なる子部分木の組合せを掛ける。

### 例題

```python
assert independent_sets([[1], [0,2], [1]], 998244353) == 5
```

[分野の目次](README.md) · [全体の目次](../README.md)
