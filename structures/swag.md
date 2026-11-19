# スライド区間集約 / Sliding Window Aggregation / SWAG

**4/5** · 末尾追加・先頭削除を償却 O(1)、区間全体の集約を O(1) で行う。

## 使い方

`SWAG(op, e)` で空のキューを作る。`op(x, y)` は左から右の順で値を結合する関数で、括り方に依存しないこと。`e` は空の集約値。例えば文字列連結なら `op=lambda x, y: x+y`、`e=""`。

`append(x)` で末尾に追加し、`popleft()` で先頭を削除してその値を返す。空のときは削除しない。`prod()` は現在の全要素を先頭から集約し、空なら `e`。

## コード

```python
class SWAG:
    def __init__(self, op, e):
        self.op, self.e = op, e
        self.front, self.back = [], []

    def append(self, x):
        prev = self.back[-1][1] if self.back else self.e
        self.back.append((x, self.op(prev, x)))

    def popleft(self):
        if not self.front:
            acc = self.e
            while self.back:
                x, _ = self.back.pop()
                acc = self.op(x, acc)
                self.front.append((x, acc))
        return self.front.pop()[0]

    def prod(self):
        a = self.front[-1][1] if self.front else self.e
        b = self.back[-1][1] if self.back else self.e
        return self.op(a, b)
```

## 考え方

区間を二つのスタックに分け、各要素にその位置までの集約を持つ。先頭側が空のときだけ末尾側を反転して移す。どの要素も高々一度しか移らない。

### 例題

```python
q = SWAG(lambda x, y: x + y, "")
for c in "abc":
    q.append(c)
assert q.popleft() == "a"
q.append("d")
assert q.prod() == "bcd"
```

[分野の目次](README.md) · [全体の目次](../README.md)
