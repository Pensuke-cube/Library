# Z アルゴリズム / Z Algorithm

**4/5** · 全位置からの接尾辞と先頭の最長共通接頭辞を O(N) で求める。

## 使い方

`z_algorithm(s)` に文字列など添字で参照できる列を渡す。戻り値 `z[i]` は、列の先頭と位置 `i` からが何要素連続で一致するか。空でない列なら `z[0] = len(s)`。空なら `[]`。

## コード

```python
def z_algorithm(s):
    n = len(s)
    if not n:
        return []
    z = [n] + [0]*(n-1)
    l = r = 0
    for i in range(1,n):
        k = min(r-i, z[i-l]) if i < r else 0
        while i+k < n and s[k] == s[i+k]:
            k += 1
        z[i] = k
        if i+k > r:
            l, r = i, i+k
    return z
```

## 考え方

先頭と一致し最も右へ伸びた区間 [l,r) を使う。内部の i では対応する先頭側の z 値が分かるので r を越える部分だけ追加で調べる。

### 例題

```python
assert z_algorithm("aabcaab") == [7,1,0,0,3,1,0]
```

[分野の目次](README.md) · [全体の目次](../README.md)
