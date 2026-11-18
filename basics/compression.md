# 座標圧縮 / Coordinate Compression

**5/5** · 値の順序を保って 0 からの連番に変換する。O(N log N)。

## 使い方

compress(a) は圧縮列、昇順の元の値を返す。

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
