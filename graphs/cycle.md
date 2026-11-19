# 有向閉路の検出・復元 / Directed Cycle Detection and Recovery

**4/5** · 有向グラフの閉路を一つ O(V+E) で見つけて復元する。

## 使い方

`directed_cycle(g)` の `g[v]` に、頂点 `v` から有向辺で直接行ける頂点番号を並べる。頂点番号は 0 始まり。閉路があれば、末尾から先頭にも辺がある巡回順の頂点リストを一つ返す。自己ループなら頂点が一つ、閉路がなければ `None`。

## コード

```python
def directed_cycle(g):
    n = len(g)
    state = bytearray(n)
    position = [-1]*n
    for s in range(n):
        if state[s]:
            continue
        state[s] = 1
        position[s] = 0
        stack = [(s,iter(g[s]))]
        while stack:
            v, it = stack[-1]
            u = next(it,None)
            if u is None:
                state[v] = 2
                stack.pop()
            elif state[u] == 1:
                return [x for x,_ in stack[position[u]:]]
            elif not state[u]:
                state[u] = 1
                position[u] = len(stack)
                stack.append((u,iter(g[u])))
    return None
```

## 考え方

各頂点を未訪問・探索中・処理済みの三状態に分ける。探索中の頂点は現在の DFS パス上にいる。そこへの辺を見つけたら、パスの対応位置から末尾までが閉路。

### 例題

```python
assert directed_cycle([[1],[2],[1,3],[]]) == [1,2]
assert directed_cycle([[1],[2],[]]) is None
```

[分野の目次](README.md) · [全体の目次](../README.md)
