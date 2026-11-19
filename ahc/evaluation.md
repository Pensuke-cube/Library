# 評価関数・差分検算・ベンチマーク / Scoring, Delta Validation and Benchmarking

**5/5** · 採点ロジックを局所で再現し、試行 K 件を O(K×採点費用) で比較する。

## 使い方

`check_delta(before, after, delta, score)` に操作前後の状態、差分計算で出した整数 `delta`、状態を丸ごと採点する関数 `score(state)` を渡す。`delta == score(after) - score(before)` を確かめ、不一致なら `AssertionError` に計算値と期待値を入れて送出する。成功時は `None`。

## コード

```python
def check_delta(before, after, delta, score):
    expected = score(after) - score(before)
    if delta != expected:
        raise AssertionError((delta, expected))
```

## 考え方

実行可能性の確認と採点を別々の関数にする。近傍ごとに差分と全再計算を照合すると、壊れた状態のまま探索を続ける事故を防げる。手法間の比較は同じ入力群で行い、スコアと時間を並べる。

### 例題

```python
a = [2,4,8]
b = [2,6,8]
check_delta(a,b,6**2-4**2,lambda s: sum(x*x for x in s))
```

[分野の目次](README.md) · [全体の目次](../README.md)
