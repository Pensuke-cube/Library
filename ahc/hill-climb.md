# 山登り法・多点スタート / Hill Climbing and Random Restarts

**5/5** · 近傍を試して改善だけ採用する。K 回の費用は O(K×近傍評価費用)。

## 使い方

`hill_climb(state, steps, propose, commit)` の `state` は変更可能な初期解、`steps` は試行回数。スコアの増加量の合計を返し、採用した変更は `state` に残る。

- `propose(state)` は状態を変更せず、`(変更後スコア − 現在スコア, 操作)` を返す。
- `commit(state, move)` は候補の操作をその場で適用する。増加量が正のときだけ呼ばれる。

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
