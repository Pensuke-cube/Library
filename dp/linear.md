# 動的計画法・状態設計 / Dynamic Programming

**5/5** · 小さい部分問題から順に答えを求める。基本の計算量は状態数×遷移数。

## 使い方

dp[i] に何を保存するか、どの状態から更新するかを先に決める。max_nonadjacent(a) は隣り合わずに選べる最大和。

## コード

```python
def max_nonadjacent(a):
    prev = best = 0
    for x in a:
        prev, best = best, max(best, prev + x)
    return best
```

## 考え方

i 番目を選ばない場合は一つ前までの最適値。選ぶ場合は二つ前までの最適値に x を足す。初期値は空集合の 0。選択を復元するなら各位置の値か遷移を残す。

### 例題

```python
assert max_nonadjacent([5, 9, 5]) == 10
```

[分野の目次](README.md) · [全体の目次](../README.md)
