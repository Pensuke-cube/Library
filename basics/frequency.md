# 辞書・集合・度数集計 / Dictionary, Set and Frequency Counting

**5/5** · 所属判定、重複除去、度数集計を平均 O(N) で行う。

## 使い方

`a` は整数や文字列など、集合の要素・辞書のキーにできる値の列。

- `set(a)` で重複を除き、`x in s` で集合 `s` に値 `x` があるか調べる。
- `Counter(a)` の `count[x]` は `x` の出現回数。未出の値は 0。
- 通常の辞書も `d.get(x, 0)` ならキー `x` が未登録のとき 0 を返す。`defaultdict(list)` ならキーごとに値をリストへ追加できる。

## コード

```python
from collections import Counter, defaultdict
```

## 考え方

順序つきの重複除去には list(dict.fromkeys(a)) を使う。集合の要素や辞書のキーにはタプルなどハッシュ可能な値を使う。

### 例題

```python
a = [3, 1, 3, 2, 1]
assert Counter(a)[3] == 2
assert list(dict.fromkeys(a)) == [3, 1, 2]
```

[分野の目次](README.md) · [全体の目次](../README.md)
