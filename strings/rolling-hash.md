# ローリングハッシュ / Rolling Hash

**4/5** · 前処理 O(N) で任意の部分文字列を O(1) でハッシュ化する。

## 使い方

RollingHash(s).get(l,r) は [l,r) のハッシュ。比較は同じ基数・同じ長さの範囲で行う。厳密一致が必要なら候補を直接比較する。

## コード

```python
class RollingHash:
    MOD = (1 << 61) - 1

    def __init__(self, s, base=1199540897363517987):
        mod = self.MOD
        self.h, self.p = h, p = [0], [1]
        for c in s:
            h.append((h[-1]*base + ord(c)+1) % mod)
            p.append(p[-1]*base % mod)

    def get(self, l, r):
        return (self.h[r] - self.h[l]*self.p[r-l]) % self.MOD
```

## 考え方

右へ伸ばすたび基数を掛け、文字を足す。左側の接頭辞の寄与を同じ桁だけずらして引く。衝突はあり得るので、敵対的な入力では実行ごとに基数を選ぶか厳密なアルゴリズムを使う。

### 例題

```python
h = RollingHash("abracadabra")
assert h.get(0,4) == h.get(7,11)
```

[分野の目次](README.md) · [全体の目次](../README.md)
