# 2-SAT・二択の制約 / 2-Satisfiability

**3/5** · 二つのリテラルの OR からなる制約を O(N+M) で解く。

## 使い方

[強連結成分分解](scc.md)のコードを先に置く。`two_sat(n, clauses)` の `n` は真偽変数の個数。各節は `(i, f, j, g)` で、`i`・`j` は 0 始まりの変数番号、`f`・`g` は真偽値。例えば `(0, True, 2, False)` は「`x[0]` が真、または `x[2]` が偽」の条件。

全ての節を満たす真偽値のリスト `x` を一つ返す。解がなければ `None`。

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
