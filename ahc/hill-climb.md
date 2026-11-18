# 山登り法・多点スタート / Hill Climbing and Random Restarts

**5/5** · 近傍を試して改善だけ採用する。K 回の費用は O(K×近傍評価費用)。

## 使い方

hill_climb(state, steps, propose, commit) は state を直接改善する。propose(state) は (スコア増分,手) を返し、状態を変更しない。

## コード

```python
def hill_climb(state, steps, propose, commit):
    gain = 0
    for _ in range(steps):
        delta, move = propose(state)
        if delta > 0:
            commit(state, move)
            gain += delta
    return gain
```

## 考え方

候補の生成、評価、確定を分ける。改善できる近傍が尽きると局所解に止まる。初期解や乱数シードを変えた複数回の探索から最良解を選べる。

### 例題

```python
a = [0]
assert hill_climb(a, 6, lambda s: (1 if s[0] < 3 else -1, 1),
                  lambda s, x: s.__setitem__(0, s[0]+x)) == 3
assert a == [3]
```

[分野の目次](README.md) · [全体の目次](../README.md)
