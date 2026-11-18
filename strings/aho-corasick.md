# 複数パターン検索 / Aho–Corasick Automaton

**3/5** · パターン総長 P のトライを使って複数パターンの出現を一度の走査で数える。

## 使い方

aho_count(text,patterns) はパターンごとの出現回数。空パターンは N+1 回、重複パターンはそれぞれ数える。

## コード

```python
def aho_count(text, patterns):
    children = [{}]
    ends = []
    for pattern in patterns:
        v = 0
        for c in pattern:
            if c not in children[v]:
                children[v][c] = len(children)
                children.append({})
            v = children[v][c]
        ends.append(v)
    fail = [0] * len(children)
    order = list(children[0].values())
    for v in order:
        for c, u in children[v].items():
            p = fail[v]
            while p and c not in children[p]:
                p = fail[p]
            fail[u] = children[p].get(c,0)
            order.append(u)

    count = [0] * len(children)
    v = 0
    for c in text:
        while v and c not in children[v]:
            v = fail[v]
        v = children[v].get(c,0)
        count[v] += 1
    for v in reversed(order):
        count[fail[v]] += count[v]
    return [count[v] if v else len(text)+1 for v in ends]
```

## 考え方

各ノードに「トライ上にも存在する最長の真接尾辞」への失敗リンクを持つ。一文字読むたび現在の接頭辞を延ばし、失敗したらリンクを辿る。走査後に逆 BFS 順で出現数を伝播する。走査は O(N+P)、疎な辞書による構築は最悪 O(P×最大パターン長)。

### 例題

```python
assert aho_count("ababa", ["aba","ba","","aba","x"]) == [2,2,6,2,0]
```

[分野の目次](README.md) · [全体の目次](../README.md)
