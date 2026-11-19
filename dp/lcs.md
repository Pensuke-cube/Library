# 最長共通部分列・編集距離 / LCS and Edit Distance

**4/5** · 二列の最長共通部分列長と編集距離をそれぞれ O(NM) で求める。

## 使い方

`a` と `b` に文字列や整数リストなど、添字で参照できて要素を等値比較できる列を渡す。

- `lcs_length(a, b)` は順序を保って両方から取り出せる共通列の最大長。取り出す位置は飛ばしてよい。
- `lcs_sequence(a, b)` はその長さを持つ実際の列をリストで返す。文字列にするなら `"".join(...)`。
- `edit_distance(a, b)` は `a` を `b` に変える挿入・削除・置換の最小回数。各操作は 1 要素ずつ行う。

## コード

```python
def lcs_length(a, b):
    if len(a) < len(b):
        a, b = b, a
    dp = [0] * (len(b)+1)
    for x in a:
        diagonal = 0
        for j, y in enumerate(b, 1):
            old = dp[j]
            dp[j] = diagonal+1 if x == y else max(old, dp[j-1])
            diagonal = old
    return dp[-1]

def lcs_sequence(a, b):
    n, m = len(a), len(b)
    dp = [[0] * (m+1) for _ in range(n+1)]
    for i, x in enumerate(a, 1):
        prev, row = dp[i-1], dp[i]
        for j, y in enumerate(b, 1):
            row[j] = prev[j-1]+1 if x == y else max(prev[j], row[j-1])
    i, j = n, m
    result = []
    while i and j:
        if a[i-1] == b[j-1]:
            result.append(a[i-1])
            i -= 1
            j -= 1
        elif dp[i-1][j] >= dp[i][j-1]:
            i -= 1
        else:
            j -= 1
    return result[::-1]

def edit_distance(a, b):
    if len(a) < len(b):
        a, b = b, a
    dp = list(range(len(b)+1))
    for i, x in enumerate(a, 1):
        diagonal, dp[0] = dp[0], i
        for j, y in enumerate(b, 1):
            old = dp[j]
            dp[j] = min(old+1, dp[j-1]+1, diagonal+(x != y))
            diagonal = old
    return dp[-1]
```

## 考え方

両列の接頭辞長を状態にする。長さや距離だけなら前の行と現在の行があればよい。復元では表の右下から始め、一致する文字を採用して斜めへ、不一致なら値が減らない方へ進む。

### 例題

```python
assert lcs_length("abca", "bda") == 2
assert "".join(lcs_sequence("abca", "bda")) == "ba"
assert edit_distance("kitten", "sitting") == 3
```

[分野の目次](README.md) · [全体の目次](../README.md)
