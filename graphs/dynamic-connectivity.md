# 辺の追加・削除を伴う連結判定 / Offline Dynamic Connectivity

**3/5** · 辺の有効期間を分割し、Q 件の操作を O(Q log Q log N) で処理する。

## 使い方

[巻き戻し Union-Find](../structures/rollback-dsu.md)を先に置く。dynamic_connectivity(n,ops) の操作は (kind,u,v)。kind は "+", "-", "?"。有効辺の重複追加や存在しない辺の削除は不可。

## コード

```python
def dynamic_connectivity(n, ops):
    q = len(ops)
    size = 1 << (max(1,q)-1).bit_length()
    tree = [[] for _ in range(2*size)]
    active = {}

    def add_interval(l, r, edge):
        l, r = l+size, r+size
        while l < r:
            if l & 1:
                tree[l].append(edge)
                l += 1
            if r & 1:
                r -= 1
                tree[r].append(edge)
            l >>= 1
            r >>= 1

    for i, (kind,u,v) in enumerate(ops):
        edge = (min(u,v), max(u,v))
        if kind == "+":
            active[edge] = i
        elif kind == "-":
            add_interval(active.pop(edge), i, edge)
    for edge,l in active.items():
        add_interval(l,q,edge)

    uf = RollbackDSU(n)
    answer = []
    def dfs(node):
        snap = uf.snapshot()
        for u,v in tree[node]:
            uf.merge(u,v)
        if node < size:
            dfs(2*node)
            dfs(2*node+1)
        elif node-size < q:
            kind,u,v = ops[node-size]
            if kind == "?":
                answer.append(uf.leader(u) == uf.leader(v))
        uf.rollback(snap)

    dfs(1)
    return answer
```

## 考え方

時刻を葉とするセグメント木を作る。各辺を有効期間に対応する O(log Q) 個のノードへ登録する。葉までの経路にある辺がその時刻の有効辺。ノードを出るときはそのノードで追加した辺を巻き戻す。

### 例題

```python
ops = [("+",0,1),("+",2,1),("?",0,2),("-",1,2),("?",0,2)]
assert dynamic_connectivity(3,ops) == [True,False]
```

[分野の目次](README.md) · [全体の目次](../README.md)
