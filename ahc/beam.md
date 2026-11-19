# ビームサーチ / Beam Search

**5/5** · 各深さで上位 B 状態だけ残す。深さ D、分岐 K の選別は O(DBK log(B+1))。

## 使い方

`beam_search(start, depth, width, expand, evaluate)` の `start` は初期状態、`depth` は何手先まで進めるか、`width` は各手で残す候補の上限（1 以上）。

- `expand(state)` はその状態から一手で作れる独立した子状態を列挙する。
- `evaluate(state)` は比較可能な評価値を返す。値が大きい状態を優先する。

指定した深さの候補を評価値の降順で返す。途中で子候補が尽きた場合は `[]`、`depth=0` なら `[start]`。

## コード

```python
from heapq import nlargest

def beam_search(start, depth, width, expand, evaluate):
    beam = [start]
    for _ in range(depth):
        children = (child for state in beam for child in expand(state))
        beam = nlargest(width, children, key=evaluate)
        if not beam:
            break
    return beam
```

## 考え方

途中状態でも将来性を評価する。確定点が同じ場合は残り手数や達成可能な上限が順位の手がかりになる。同じ深さの等価状態は一つにまとめると有効な幅が増える。手順復元には親への参照を持てる。

### 例題

```python
# ±1 を 3 回足し、4 に最も近づける。
ans = beam_search(0, 3, 2, lambda x: (x-1,x+1), lambda x: -abs(4-x))
assert ans[0] == 3
```

[分野の目次](README.md) · [全体の目次](../README.md)
