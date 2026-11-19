# 部分集合ゼータ・メビウス変換 / Subset Zeta and Möbius Transform

**3/5** · 全マスクについて部分マスクの和をまとめる。O(N2^N)。

## 使い方

`subset_transform(a, inverse=False)` に長さが 2 のべき乗の数値リストを渡す。添字は集合を表すビットマスク。`inverse=False` では各 `a[mask]` を `mask` の全ての部分マスクに対応する値の和に置き換える。変換後の同じリストに `inverse=True` を指定すると元に戻る。戻り値は `None`。

## コード

```python
def subset_transform(a, inverse=False):
    n = len(a)
    step = 1
    sign = -1 if inverse else 1
    while step < n:
        for start in range(0, n, step * 2):
            for i in range(start + step, start + 2*step):
                a[i] += sign * a[i-step]
        step *= 2
```

## 考え方

ビット i を一つずつ自由にし、そのビットを落とした集合の集計値を足す。逆変換は引く。上位集合の和なら伝播方向を逆にする。

### 例題

```python
a = [1,2,3,4]
subset_transform(a)
assert a == [1,3,4,10]
subset_transform(a, inverse=True)
assert a == [1,2,3,4]
```

[分野の目次](README.md) · [全体の目次](../README.md)
