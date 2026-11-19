# 座標圧縮 / Coordinate Compression

**5/5** · 値の順序を保って 0 からの連番に変換する。O(N log N)。

## 使い方

`compress(a)` に順序比較とハッシュができる値の列 `a` を渡す。`(ranks, values)` を返し、`values` は重複を除いた昇順リスト。`ranks[i]` は元の `a[i]` を `values` 内の 0 始まりの位置に置き換えた値で、`values[ranks[i]]` で元に戻せる。

## コード

```python
def compress(a):
    a = list(a)
    values = sorted(set(a))
    rank = {x: i for i, x in enumerate(values)}
    return [rank[x] for x in a], values
```

## 考え方

添字を小さくして Fenwick 木などを使える。座標間の距離が要るときは values[i+1]-values[i] を使う。クエリの境界も圧縮対象に入れるか二分探索で挿入位置を求める。

### 例題

```python
assert compress([100, -4, 100, 8]) == ([2, 0, 2, 1], [-4, 8, 100])
```

[分野の目次](README.md) · [全体の目次](../README.md)
