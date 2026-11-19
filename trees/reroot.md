# 全方位木 DP / Rerooting DP

**4/5** · 全ての頂点を根とした答えを O(N) でまとめて求める。

## 使い方

[根付き化](euler-tour.md)のコードを先に置く。`distance_sums(g)` に空でない無向木を渡す。`g[v]` は 0 始まりの頂点 `v` の隣接リストで、各辺を両方向に登録する。戻り値 `ans[v]` は `v` から全頂点への距離の和。各辺の長さを 1 とし、自分自身までの距離は 0。

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
