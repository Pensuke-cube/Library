# 接尾辞配列・LCP 配列 / Suffix Array and LCP Array

**3/5** · 接尾辞の辞書順を O(N log² N)、隣接接尾辞の共通接頭辞長を O(N) で求める。

## 使い方

- `suffix_array(s)` に文字列を渡す。`s[i:]` が辞書順になるよう並べた 0 始まりの添字列 `sa` を返す。空の接尾辞は含めない。
- `lcp_array(s, sa)` に同じ文字列と、その `suffix_array(s)` の結果を渡す。`lcp[i]` は辞書順で隣り合う `s[sa[i]:]` と `s[sa[i+1]:]` の先頭が何文字一致するか。

## コード

```python
def suffix_array(s):
    n = len(s)
    sa = list(range(n))
    rank = [ord(c) for c in s]
    width = 1
    while width < n:
        next_rank = rank[width:] + [-1]*width
        keys = list(zip(rank, next_rank))
        sa.sort(key=keys.__getitem__)
        rank = [0] * n
        group = 0
        for a, b in zip(sa, sa[1:]):
            group += keys[a] != keys[b]
            rank[b] = group
        if group == n-1:
            break
        width *= 2
    return sa

def lcp_array(s, sa):
    n = len(s)
    rank = [0] * n
    for i, j in enumerate(sa):
        rank[j] = i
    lcp = [0] * max(0, n-1)
    common = 0
    for i in range(n):
        r = rank[i]
        if r == 0:
            common = 0
            continue
        j = sa[r-1]
        while i+common < n and j+common < n and s[i+common] == s[j+common]:
            common += 1
        lcp[r-1] = common
        common = max(0, common-1)
    return lcp
```

## 考え方

長さ k の順位の対で長さ 2k を比較する。LCP は両方の先頭を 1 文字落としても共通長が高々 1 しか減らない性質を使う。異なる部分文字列数は N(N+1)/2 から LCP の総和を引いた値。

### 例題

```python
s = "banana"
sa = suffix_array(s)
assert sa == [5,3,1,0,4,2] and lcp_array(s,sa) == [1,3,0,0,2]
```

[分野の目次](README.md) · [全体の目次](../README.md)
