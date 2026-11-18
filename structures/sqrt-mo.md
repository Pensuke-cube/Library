# 平方分割・Mo のアルゴリズム / Square-Root Decomposition and Mo's Algorithm

**3/5** · 静的な区間クエリを O(Q log Q+(N+Q)√N) の目安で処理する。

## 使い方

mo_distinct(a,queries) は半開区間ごとの異なる値の数。a の要素はハッシュ可能。

## コード

```python
from math import isqrt

def mo_distinct(a, queries):
    queries = list(queries)
    block = max(1, isqrt(len(a)))
    def key(i):
        l, r = queries[i]
        b = l // block
        return b, -r if b & 1 else r

    rank = {x: i for i,x in enumerate(set(a))}
    a = [rank[x] for x in a]
    freq = [0] * len(rank)
    answer = [0] * len(queries)
    l = r = distinct = 0
    for i in sorted(range(len(queries)), key=key):
        left, right = queries[i]
        while l > left:
            l -= 1
            x = a[l]
            distinct += freq[x] == 0
            freq[x] += 1
        while r < right:
            x = a[r]
            distinct += freq[x] == 0
            freq[x] += 1
            r += 1
        while l < left:
            x = a[l]
            freq[x] -= 1
            distinct -= freq[x] == 0
            l += 1
        while r > right:
            r -= 1
            x = a[r]
            freq[x] -= 1
            distinct -= freq[x] == 0
        answer[i] = distinct
    return answer
```

## 考え方

左端を幅 B のブロックに分け、同じブロックでは右端を単調に動かす。左右移動量は O(QB+N²/B)。通常の平方分割では列自体をブロックに分け、クエリ両端は個別、中間はブロック集約で処理する。

### 例題

```python
assert mo_distinct([1,2,1,4], [(0,4),(0,3),(2,2),(2,4)]) == [3,2,0,2]
```

[分野の目次](README.md) · [全体の目次](../README.md)
