# 焼きなまし法 / Simulated Annealing

**5/5** · 改善に加えて一部の悪化を受理し、局所解から抜け出す。K 回の費用は O(K×近傍評価費用)。

## 使い方

anneal(state,score,steps,t0,t1,propose,commit,clone,rng) は最大化用。t0,t1>0。propose(state,rng) は状態を変えず (増分,手) を返す。clone は独立な複製。

## コード

```python
from math import exp, log
from random import Random

def anneal(state, score, steps, t0, t1, propose, commit, clone, rng):
    best, best_score = clone(state), score
    cool = log(t1) - log(t0)
    for i in range(steps):
        delta, move = propose(state, rng)
        temperature = t0 * exp(cool * i / max(1, steps-1))
        if delta >= 0 or rng.random() < exp(delta / temperature):
            commit(state, move)
            score += delta
            if score > best_score:
                best, best_score = clone(state), score
    return best, best_score
```

## 考え方

悪化量 d が正なら受理率は exp(-d/T)。序盤は近傍の代表的な悪化量を参考に温度を選び、終盤は改善をほぼ優先する。制限時間に合わせる場合は i/(steps-1) を経過時間の割合に置き換える。

### 例題

```python
# x を動かして -(x-4)^2 を最大化。
def propose(s, rng):
    x = s[0] + rng.choice((-1,1))
    return (s[0]-4)**2 - (x-4)**2, x

best, score = anneal([0], -16, 100, 3, 0.1, propose,
                     lambda s,x: s.__setitem__(0,x), list.copy, Random(1))
assert best == [4] and score == 0
```

[分野の目次](README.md) · [全体の目次](../README.md)
