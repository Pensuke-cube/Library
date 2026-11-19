# ゲーム DP・Grundy 数 / Game DP and Sprague–Grundy Numbers

**4/5** · 手詰まりで負ける公平な有限ゲームを DAG の状態と遷移に比例する時間で解く。

## 使い方

`grundy(g, order)` の `g[v]` は状態 `v` から一手で移れる状態番号のリスト。状態番号は 0 始まり。行き先のない状態では負けとする。`order` にすべての状態を、各移動の行き先が後ろに来る順で渡す。結果の `values[v]` が状態 `v` の Grundy 数で、一つのゲームでは 0 が負け状態。

## コード

```python
def grundy(g, order):
    values = [0] * len(g)
    for v in reversed(order):
        used = {values[u] for u in g[v]}
        k = 0
        while k in used:
            k += 1
        values[v] = k
    return values
```

## 考え方

遷移先の Grundy 数の集合に含まれない最小非負整数を取る。独立な複数ゲームから毎手一つだけ操作するなら、各 Grundy 数の XOR が 0 の状態が負け。

### 例題

```python
# 石を 1 個または 2 個取り、最後に取った人が勝つ。
g = [[n-x for x in (1,2) if n >= x] for n in range(6)]
assert grundy(g, list(reversed(range(6)))) == [0,1,2,0,1,2]
```

[分野の目次](README.md) · [全体の目次](../README.md)
