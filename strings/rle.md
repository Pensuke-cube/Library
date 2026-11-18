# ランレングス圧縮 / Run-Length Encoding

**5/5** · 同じ値が連続する区間を (値,長さ) にする。O(N)。

## 使い方

run_length(a) は列やイテレータを受け取り、順に連続区間を返す。

## コード

```python
from itertools import groupby

def run_length(a):
    return [(x, sum(1 for _ in run)) for x, run in groupby(a)]
```

## 考え方

同じ値が離れて現れた場合は別の区間。連続する区間だけに依存する処理なら、元の位置を長さの累積で求められる。

### 例題

```python
assert run_length("aaabbba") == [("a",3), ("b",3), ("a",1)]
```

[分野の目次](README.md) · [全体の目次](../README.md)
