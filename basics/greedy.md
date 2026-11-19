# 貪欲法・区間スケジューリング / Greedy / Interval Scheduling

**5/5** · 終了時刻順の貪欲法で共通部分を持たない半開区間を最大個数選ぶ。O(N log N)。

## 使い方

`interval_schedule(intervals)` に `(l, r)` の列を渡す。`l` は開始、`r` は終了で `l < r`。時刻 `r` から始まる次の区間とは重ならない。重ならずに選べる区間の組のうち、個数が最大の一組を終了時刻順で返す。

## コード

```python
def interval_schedule(intervals):
    result = []
    for l, r in sorted(intervals, key=lambda p: p[1]):
        if not result or result[-1][1] <= l:
            result.append((l, r))
    return result
```

## 考え方

最適解の最初の区間を最も早く終わる区間と交換しても、残りの区間は置ける。一般の貪欲法も交換や不変条件で正しさを示す。区間に重みがある最大和は DP を使う。

### 例題

```python
assert interval_schedule([(1, 4), (0, 2), (2, 3), (4, 5)]) == [(0, 2), (2, 3), (4, 5)]
```

[分野の目次](README.md) · [全体の目次](../README.md)
