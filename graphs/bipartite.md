# 二部グラフ判定 / Bipartite Graph Test

**4/5** · 無向グラフを隣同士で色が違う二色に塗れるか O(V+E) で判定する。

## 使い方

bipartite(g) は 0/1 の色配列を返す。塗れなければ None。

## コード

```python
def bipartite(g):
    color = [-1] * len(g)
    for s in range(len(g)):
        if color[s] != -1:
            continue
        color[s] = 0
        stack = [s]
        while stack:
            v = stack.pop()
            other = color[v] ^ 1
            for u in g[v]:
                if color[u] == -1:
                    color[u] = other
                    stack.append(u)
                elif color[u] != other:
                    return None
    return color
```

## 考え方

辺を渡るたび色を反転する。矛盾があれば奇数長の閉路がある。非連結なら各成分の色は独立に反転できる。

### 例題

```python
assert bipartite([[1], [0], []]) == [0, 1, 0]
assert bipartite([[1, 2], [0, 2], [0, 1]]) is None
```

[分野の目次](README.md) · [全体の目次](../README.md)
