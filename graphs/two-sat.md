# 2-SAT・二択の制約 / 2-Satisfiability

**3/5** · 二つのリテラルの OR からなる制約を O(N+M) で解く。

## 使い方

[強連結成分分解](scc.md)を先に置く。two_sat(n,clauses) の節は (i,f,j,g) で (x[i]==f or x[j]==g)。不能なら None。

## コード

```python
def two_sat(n, clauses):
    graph = [[] for _ in range(2 * n)]
    for i, f, j, g in clauses:
        a, b = 2 * i + int(f), 2 * j + int(g)
        graph[a ^ 1].append(b)
        graph[b ^ 1].append(a)
    ids, _ = scc(graph)
    if any(ids[2*i] == ids[2*i+1] for i in range(n)):
        return None
    return [ids[2*i] < ids[2*i+1] for i in range(n)]
```

## 考え方

a∨b は ¬a→b と ¬b→a。ある命題と否定が同じ成分なら矛盾。そうでなければ DAG の後ろ側のリテラルを真にする。

### 例題

```python
assert two_sat(2, [(0, True, 0, True), (0, False, 1, True)]) == [True, True]
assert two_sat(1, [(0, True, 0, True), (0, False, 0, False)]) is None
```

[分野の目次](README.md) · [全体の目次](../README.md)
