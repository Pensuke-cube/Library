# 直線最小値・Li Chao 木 / Li Chao Tree

**3/5** · 直線を追加し、既知の x における最小値を各 O(log N) で求める。

## 使い方

`LiChao(xs)` に照会で使う x 座標をすべて渡す。重複は可。

- `add(a, b)` は傾き `a`、切片 `b` の直線 `y = a*x + b` を追加する。
- `query(x)` は指定座標で全登録直線の中の最小の y を返す。`x` は `xs` に入っている値。直線がなければ `float("inf")`、未登録の座標なら `KeyError`。

## コード

```python
from bisect import bisect_left

class LiChao:
    def __init__(self, xs):
        self.xs = sorted(set(xs))
        self.lines = [None] * (4 * len(self.xs))

    def add(self, a, b):
        xs, lines = self.xs, self.lines
        i, l, r = 1, 0, len(xs)
        while l < r:
            if lines[i] is None:
                lines[i] = (a,b)
                return
            c, d = lines[i]
            m = (l+r)//2
            better_left = a*xs[l]+b < c*xs[l]+d
            better_mid = a*xs[m]+b < c*xs[m]+d
            if better_mid:
                lines[i], a, b = (a,b), c, d
            if r-l == 1:
                return
            if better_left != better_mid:
                i, r = 2*i, m
            else:
                i, l = 2*i+1, m

    def query(self, x):
        xs = self.xs
        p = bisect_left(xs,x)
        if p == len(xs) or xs[p] != x:
            raise KeyError(x)
        ans = float("inf")
        i, l, r = 1, 0, len(xs)
        while self.lines[i] is not None:
            a, b = self.lines[i]
            ans = min(ans, a*x+b)
            if r-l == 1:
                break
            m = (l+r)//2
            if p < m:
                i, r = 2*i, m
            else:
                i, l = 2*i+1, m
        return ans
```

## 考え方

中央で小さい直線をそのノードに残す。二直線の優劣は高々一度入れ替わるので、残りが勝てる側だけに降ろす。DP が dp[i]=min_j(a[j]·x[i]+b[j]) の形なら、j の処理後に直線を足す。

### 例題

```python
lc = LiChao([-5,0,3])
lc.add(1,2)
lc.add(-2,5)
assert [lc.query(x) for x in [-5,0,3]] == [-3,2,-1]
```

[分野の目次](README.md) · [全体の目次](../README.md)
