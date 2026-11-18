# バックトラック・枝刈り / Backtracking and Pruning

**4/5** · 候補木を探索し、完成できない枝を早期に除く。最悪計算量は探索木に依存。

## 使い方

使った要素の印を戻しながら探索する。下の例は正整数から和が target になる選び方を数える。

## コード

```python
def count_subsets(a, target):
    def dfs(i, remain):
        if remain == 0:
            return 1
        if remain < 0 or i == len(a):
            return 0
        return dfs(i + 1, remain) + dfs(i + 1, remain - a[i])
    return dfs(0, target)
```

## 考え方

残りが負なら正整数を足して到達できない。同じ状態が何度も現れるならメモ化し、深さが大きいときはスタックで処理する。

### 例題

```python
# 5 を作る方法は 2+3 と 5。
assert count_subsets([2, 3, 5], 5) == 2
```

[分野の目次](README.md) · [全体の目次](../README.md)
