# トライ木・接頭辞の個数 / Trie

**4/5** · 文字列を長さに比例する時間で追加し、接頭辞に一致する個数を求める。

## 使い方

`Trie()` で空の辞書を作る。`add(word)` に文字列を渡して登録し、`prefix_count(prefix)` に調べたい先頭文字列を渡す。戻り値はその文字列で始まる登録語の数。同じ語を複数回登録するとその回数分だけ増え、空の接頭辞なら全登録数。

## コード

```python
class Trie:
    def __init__(self):
        self.children = [{}]
        self.count = [0]

    def add(self, word):
        v = 0
        self.count[v] += 1
        for c in word:
            u = self.children[v].get(c)
            if u is None:
                u = len(self.children)
                self.children[v][c] = u
                self.children.append({})
                self.count.append(0)
            v = u
            self.count[v] += 1

    def prefix_count(self, prefix):
        v = 0
        for c in prefix:
            v = self.children[v].get(c)
            if v is None:
                return 0
        return self.count[v]
```

## 考え方

各ノードは一つの接頭辞に対応する。単語全体の一致も欲しいなら末端で止まった個数を別に持つ。辞書順の連続範囲だけで足りる場合は整列して二分探索する手もある。

### 例題

```python
t = Trie()
for s in ["at", "atom", "as"]:
    t.add(s)
assert t.prefix_count("at") == 2 and t.prefix_count("b") == 0
```

[分野の目次](README.md) · [全体の目次](../README.md)
