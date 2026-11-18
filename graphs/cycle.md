# 有向閉路の検出・復元 / Directed Cycle Detection and Recovery

**4/5** · 有向グラフの閉路を一つ O(V+E) で見つけて復元する。

## 使い方

directed_cycle(g) は閉路上の頂点を巡回順で返す。閉路なしは None。先頭を末尾に重ねない。

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
