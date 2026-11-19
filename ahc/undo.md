# 可逆な状態更新・ロールバック / Reversible Moves and Rollback

**4/5** · 候補を適用して評価し、変更箇所だけを元に戻す。K 箇所の更新と復元は O(K)。

## 使い方

`run_trial(state, move, apply, undo, evaluate)` に変更可能な状態 `state` と試す操作 `move` を渡す。操作を適用した状態の評価値を返し、状態を元に戻す。

- `apply(state, move)` は状態を変更し、古い値などの復元記録を返す。
- `undo(state, record)` はその記録を使い、状態をその場で元に戻す。
- `evaluate(state)` は変更後の状態を受け取り、評価値を返す。

## コード

```python
def run_trial(state, move, apply, undo, evaluate):
    record = apply(state,move)
    try:
        return evaluate(state)
    finally:
        undo(state,record)
```

## 考え方

各候補で配列全体をコピーする代わりに、更新した添字と古い値を記録する。同じ場所を複数回変更する場合は逆順に戻す。採用した候補だけ確定し、状態と補助スコアの両方に同じ操作を反映する。

### 例題

```python
def change(a, move):
    i,x = move
    old = a[i]
    a[i] = x
    return i,old

a = [1,3,5]
assert run_trial(a,(1,4),change,change,sum) == 10
assert a == [1,3,5]
```

[分野の目次](README.md) · [全体の目次](../README.md)
