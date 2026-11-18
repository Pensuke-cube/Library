# ビット集合による到達性 / Bitset Reachability

**3/5** · DAG の各頂点からの到達先を逆トポロジカル順のビット OR で求める。

## 使い方

[トポロジカルソート](toposort.md)を先に置く。dag_reachability(g) の戻り値 bits[v] の u ビットで到達判定。自分自身も含む。

## コード

```python
def dag_reachability(g):
    bits = [0] * len(g)
    for v in reversed(toposort(g)):
        state = 1 << v
        for u in g[v]:
            state |= bits[u]
        bits[v] = state
    return bits
```

## 考え方

v から行ける先は v 自身と各行き先の到達集合の和集合。内部桁幅 w として O((V+E)⌈V/w⌉) が目安。全頂点対が不要なら、質問の到達先だけをビットに割り当て、一定個数ずつ処理するとメモリを抑えられる。一般の有向グラフは強連結成分を縮約する。

### 例題

```python
b = dag_reachability([[1,2], [3], [], []])
assert b[0] == 15 and b[1] == 10 and b[2] == 4
```

[分野の目次](README.md) · [全体の目次](../README.md)
