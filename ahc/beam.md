# ビームサーチ / Beam Search

**5/5** · 各深さで上位 B 状態だけ残す。深さ D、分岐 K の選別は O(DBK log(B+1))。

## 使い方

beam_search(start,depth,width,expand,evaluate) は各層の状態を高評価順に返す。expand(state) は独立した子状態の列。width≥1。

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
