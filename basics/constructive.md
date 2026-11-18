# 構築・不変量 / Constructive Algorithms and Invariants

**4/5** · 達成条件を式に直して実例を作る。例は N 個の整数を O(N) で構築。

## 使い方

distinct_zero_sum(n) は相異なる n 個の整数で和が 0 の列を作る。

## コード

```python
def distinct_zero_sum(n):
    a = []
    for x in range(1, n//2+1):
        a.extend((x, -x))
    if n & 1:
        a.append(0)
    return a
```

## 考え方

和 0 の部品を作って並べる。数の個数と相異性が自動で保たれる。操作問題では和・偶奇・連結性など操作で変わらない量を探し、必要条件から逆に構成できるか調べる。

### 例題

```python
a = distinct_zero_sum(7)
assert len(a) == len(set(a)) == 7 and sum(a) == 0
```

[分野の目次](README.md) · [全体の目次](../README.md)
