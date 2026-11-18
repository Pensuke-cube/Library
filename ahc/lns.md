# 大近傍探索・壊して作り直す / Large Neighborhood Search

**4/5** · 解の一部を外して再構築する。K 回の費用はコピー・修復・評価の K 回分。

## 使い方

lns(state,steps,rebuild,score,rng) で最大化。rebuild(state,rng) は元の状態を変更せず、実行可能な候補を返す。

## コード

```python
def lns(state, steps, rebuild, score, rng):
    value = score(state)
    for _ in range(steps):
        candidate = rebuild(state, rng)
        nd = score(candidate)
        if nd > value:
            state, value = candidate, nd
    return state, value
```

## 考え方

局所探索で動かしづらい複数要素をまとめて外す。修復は貪欲、区間 DP、短い全探索などを使う。破壊範囲が大きいほど候補は変化するが、一回の費用も増える。

### 例題

```python
from random import Random

def repair(a, rng):
    i = rng.randrange(len(a)-1)
    return a[:i] + sorted(a[i:i+2]) + a[i+2:]

def score(a):
    return -sum(x > y for i,x in enumerate(a) for y in a[i+1:])

assert lns([3,2,1], 100, repair, score, Random(0)) == ([1,2,3],0)
```

[分野の目次](README.md) · [全体の目次](../README.md)
