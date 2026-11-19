# 回文半径・Manacher 法 / Manacher's Algorithm

**3/5** · 奇数長・偶数長回文の最大半径を全中心について O(N) で求める。

## 使い方

`manacher(s)` に文字列を渡し、同じ長さのリスト二つ `(odd, even)` を受け取る。

- `odd[i]` は文字 `s[i]` を中心とする回文の片側長（中心を含む）。回文は `s[i-odd[i]+1 : i+odd[i]]`。
- `even[i]` は添字 `i-1` と `i` の間を中心とする回文の片側長。回文は `s[i-even[i] : i+even[i]]` で、該当する空でない回文がなければ 0。

## コード

```python
def manacher(s):
    n = len(s)
    result = []
    for gap in (0,1):
        radius = [0] * n
        l, r = 0, -1
        for i in range(n):
            k = min(radius[l+r-i+gap], r-i+1) if i <= r else 1-gap
            while i-k-gap >= 0 and i+k < n and s[i-k-gap] == s[i+k]:
                k += 1
            radius[i] = k
            if i+k-1 > r:
                l, r = i-k+1-gap, i+k-1
        result.append(radius)
    return tuple(result)
```

## 考え方

最も右へ伸びた回文の中では中心の反対側にある半径を再利用する。奇数長は 2·odd[i]-1、偶数長は 2·even[i]。半径の和は空でない回文部分文字列の総数になる。

### 例題

```python
odd, even = manacher("abba")
assert odd == [1,1,1,1] and even == [0,0,2,0]
```

[分野の目次](README.md) · [全体の目次](../README.md)
