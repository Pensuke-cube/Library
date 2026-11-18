# 全方位木 DP / Rerooting DP

**4/5** · 全ての頂点を根とした答えを O(N) でまとめて求める。

## 使い方

[根付き化](euler-tour.md)を先に置く。distance_sums(g) は各頂点から全頂点への辺数距離の和。

## コード

```python
def distance_sums(g):
    parent, depth, order, _, _ = root_tree(g)
    n = len(g)
    size = [1] * n
    for v in reversed(order[1:]):
        size[parent[v]] += size[v]
    ans = [0] * n
    ans[0] = sum(depth)
    for v in order[1:]:
        ans[v] = ans[parent[v]] + n - 2 * size[v]
    return ans
```

## 考え方

根を子へ移すと、その部分木内は距離が 1 縮み、外は 1 伸びる。一般形では辺の両向きに DP 値を持つ。各隣接部分の集約を前後の累積で求めれば、特定の子を除く計算も全体で O(N)。

### 例題

```python
assert distance_sums([[1,2,3], [0], [0], [0]]) == [3,5,5,5]
```

[分野の目次](README.md) · [全体の目次](../README.md)
