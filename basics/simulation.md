# シミュレーション・周期検出 / Simulation and Cycle Detection

**4/5** · 決定的な遷移の T 回後を、出現した状態数までの計算で求める。

## 使い方

iterate_state(start, step, t) は遷移 t 回後の状態。状態はハッシュ可能にする。

## コード

```python
def iterate_state(start, step, t):
    seen = {}
    states = []
    state = start
    while t and state not in seen:
        seen[state] = len(states)
        states.append(state)
        state = step(state)
        t -= 1
    if t:
        begin = seen[state]
        return states[begin + t % (len(states) - begin)]
    return state
```

## 考え方

同じ状態が再出現したら以降の遷移列も同じ。必要な累積値があれば前周期と一周期分の差を記録する。時刻で遷移が変わる場合は時刻の位相も状態に含める。

### 例題

```python
assert iterate_state(0, lambda x: (x + 2) % 7, 10**12) == 2 * 10**12 % 7
```

[分野の目次](README.md) · [全体の目次](../README.md)
