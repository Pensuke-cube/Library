# ソートと順序付け / Sorting and Ordering

**5/5** · 要素をキー順に整列する。比較ソート O(N log N)、計数ソート O(N+K)。

## 使い方

- `sorted(a, key=...)` は列 `a` を並べ替えた新しいリストを返す。リストをその場で整列するには `a.sort(key=...)`。`key` は要素を一つ受け取り、比較に使う値を返す関数。省略すると要素自体を比較する。
- `counting_sort(a, k)` に整数列と値域の上端 `k` を渡す。全要素が `0 <= x < k` のとき、新しい昇順リストを返す。

## コード

```python
def counting_sort(a, k):
    count = [0] * k
    for x in a:
        count[x] += 1
    return [x for x, c in enumerate(count) for _ in range(c)]
```

## 考え方

Python のソートは安定。例えば点数降順・番号昇順ならキーを (-score, id) にする。値が 0 以上 K 未満で K が小さいときは度数から復元できる。

### 例題

```python
assert sorted([(2, 8), (1, 8), (3, 9)], key=lambda p: (-p[1], p[0])) == [(3, 9), (1, 8), (2, 8)]
assert counting_sort([2, 0, 2, 1], 3) == [0, 1, 2, 2]
```

[分野の目次](README.md) · [全体の目次](../README.md)
