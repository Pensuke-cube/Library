# 二進トライ・XOR 最小値 / Binary Trie and Minimum XOR

**3/5** · 非負整数を追加し、指定値との XOR の最小値を O(B) で求める。

## 使い方

`BinaryTrie(bits)` で空の集合を作る。`bits` は扱うビット数で、各値は `0 <= x < 2**bits` の整数。

- `add(x)` で値 `x` を登録する。
- `min_xor(x)` は登録値 `y` のうち `x ^ y` が最小になるときの XOR 値を返す。空なら `None`。

## コード

```python
class BinaryTrie:
    def __init__(self, bits):
        self.bits = bits
        self.next = [[-1,-1]]
        self.size = 0

    def add(self, x):
        node = 0
        for i in range(self.bits-1,-1,-1):
            b = x >> i & 1
            child = self.next[node][b]
            if child < 0:
                child = len(self.next)
                self.next[node][b] = child
                self.next.append([-1,-1])
            node = child
        self.size += 1

    def min_xor(self, x):
        if not self.size:
            return None
        node = result = 0
        for i in range(self.bits-1,-1,-1):
            b = x >> i & 1
            child = self.next[node][b]
            if child < 0:
                result |= 1 << i
                child = self.next[node][b^1]
            node = child
        return result
```

## 考え方

上位ビット一つの差はそれより下の全ビットの合計より大きい。その桁が一致する枝があれば優先する。削除を扱うなら各ノードの通過個数を持つ。

### 例題

```python
t = BinaryTrie(5)
assert t.min_xor(7) is None
t.add(10)
t.add(6)
assert t.min_xor(7) == 1
```

[分野の目次](README.md) · [全体の目次](../README.md)
