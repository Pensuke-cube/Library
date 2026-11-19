# KMP 法・文字列の周期 / Knuth–Morris–Pratt Algorithm

**4/5** · パターンの全出現位置と接頭辞の境界を O(N+M) で求める。

## 使い方

- `kmp(text, pattern)` に検索対象と探したい文字列を渡す。一致が始まる 0 始まりの位置を昇順に列挙する。重なる一致も含み、空パターンなら `0` から `len(text)` の全境界。リストが必要なら `list(kmp(text, pattern))`。
- `prefix_function(s)` の `p[i]` は `s[:i+1]` の先頭と末尾で一致する最長の文字数。接頭辞全体と同じ長さは候補から除く。

## コード

```python
def prefix_function(s):
    p = [0] * len(s)
    j = 0
    for i in range(1,len(s)):
        while j and s[i] != s[j]:
            j = p[j-1]
        if s[i] == s[j]:
            j += 1
        p[i] = j
    return p

def kmp(text, pattern):
    if not pattern:
        yield from range(len(text)+1)
        return
    p = prefix_function(pattern)
    j = 0
    for i, c in enumerate(text):
        while j and c != pattern[j]:
            j = p[j-1]
        if c == pattern[j]:
            j += 1
        if j == len(pattern):
            yield i-j+1
            j = p[j-1]
```

## 考え方

p[i] は s[:i+1] の接頭辞でも接尾辞でもある最長の真部分列の長さ（連続部分）。不一致なら次に短い境界に戻る。空でない列が短い列の反復かは k=N-p[-1] が N を割るかで判定できる。

### 例題

```python
assert list(kmp("ababa", "aba")) == [0,2]
s = "abcabc"
assert len(s) - prefix_function(s)[-1] == 3
```

[分野の目次](README.md) · [全体の目次](../README.md)
