# ダブリング / Binary Lifting / Doubling

**4/5** · 決定的な遷移の K 回先を、前処理 O(N log K) 後に O(log K) で求める。

## 使い方

`doubling(nxt, max_k)` に遷移先のリストと最大の遷移回数 `max_k`（0 以上の整数）を渡す。`nxt[v]` は地点 `v` から一回進む先で、`0 <= nxt[v] < len(nxt)`。

`jump(table, v, k)` に作った表、出発地点 `v`、回数 `k` を渡す。`0 <= k <= max_k` で、`v` からちょうど `k` 回進んだ地点を返す。

## コード

```python
def doubling(nxt, max_k):
    table = [list(nxt)]
    for _ in range(1, max_k.bit_length()):
        prev = table[-1]
        table.append([prev[x] for x in prev])
    return table

def jump(table, v, k):
    while k:
        low = k & -k
        v = table[low.bit_length() - 1][v]
        k ^= low
    return v
```

## 考え方

2^i 回の行き先は 2^(i-1) 回を二度適用する。遷移ごとの加点も同じ表に持てる。始点が一つなら周期検出で O(N) にできることがある。

### 例題

```python
assert jump(doubling([1, 2, 3, 1], 100), 0, 100) == 1
```

[分野の目次](README.md) · [全体の目次](../README.md)
