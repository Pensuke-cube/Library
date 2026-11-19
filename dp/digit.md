# 桁 DP / Digit DP

**4/5** · 上限以下の整数を上位桁から数える。O(桁数×状態数×基数)。

## 使い方

`count_digit_sum(bound, d)` に上限を表す空でない十進数字列（例 `"200"`）と正整数 `d` を渡す。0 以上・上限以下で、各桁の和が `d` で割り切れる整数の個数を返す。0 も数え、剰余は取らない。

## コード

```python
def count_digit_sum(bound, d):
    loose = [0] * d
    tight_sum = 0
    for c in bound:
        digit = int(c)
        nxt = [0] * d
        for rem, count in enumerate(loose):
            for x in range(10):
                nxt[(rem+x) % d] += count
        for x in range(digit):
            nxt[(tight_sum+x) % d] += 1
        tight_sum = (tight_sum + digit) % d
        loose = nxt
    return loose[0] + (tight_sum == 0)
```

## 考え方

上限と同じ接頭辞なら次の桁は上限の桁以下。小さくなった状態は以後自由。先頭の 0 を許して桁数を揃える。桁が非常に多く剰余解が必要なら各更新で剰余を取る。

### 例題

```python
assert count_digit_sum("20", 3) == 7
```

[分野の目次](README.md) · [全体の目次](../README.md)
