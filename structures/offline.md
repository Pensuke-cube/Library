# オフラインクエリ・ソートで処理 / Offline Query Processing

**4/5** · クエリを並べ替えて共有部分を使い、値の閾値つき区間件数を O((N+Q)log(N+Q)) で求める。

## 使い方

[Fenwick 木](fenwick.md)を先に置く。count_le_queries(a,queries) は (l,r,x) ごとに [l,r) 内の x 以下の個数。

## コード

```python
def count_le_queries(a, queries):
    queries = list(queries)
    points = sorted(range(len(a)), key=a.__getitem__)
    order = sorted(range(len(queries)), key=lambda i: queries[i][2])
    bit = Fenwick(len(a))
    answer = [0] * len(queries)
    j = 0
    for i in order:
        l, r, x = queries[i]
        while j < len(a) and a[points[j]] <= x:
            bit.add(points[j], 1)
            j += 1
        answer[i] = bit.sum(l, r)
    return answer
```

## 考え方

閾値の小さい質問から処理して、有効な位置を増やす。元の質問番号を持てば出力順を戻せる。クエリが直前の出力に依存する場合は先読みできない。

### 例題

```python
assert count_le_queries([4,1,3,1], [(0,4,3),(1,3,1),(0,2,0)]) == [3,1,0]
```

[分野の目次](README.md) · [全体の目次](../README.md)
