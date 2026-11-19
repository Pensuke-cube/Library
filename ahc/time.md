# 時間管理・乱数の再現 / Time Budget and Reproducibility

**5/5** · 実行時間と試行回数を管理する。時刻確認を B 回に一度にまとめる。

## 使い方

`run_batches(seconds, batch, step)` に時間枠 `seconds`（0 以上の秒数）、時計を確認する間隔 `batch`（1 以上の整数）、一回分の処理 `step()` を渡す。`step()` を呼んだ回数を返し、`step()` の戻り値は使わない。時間切れはバッチ間で確認する。例えば `batch=16` なら 16 回呼ぶごとに確認する。

## コード

```python
from time import perf_counter
from random import Random

def run_batches(seconds, batch, step):
    end = perf_counter() + seconds
    count = 0
    while perf_counter() < end:
        for _ in range(batch):
            step()
        count += batch
    return count
```

## 考え方

時間切れはバッチの境界で検出するため、バッチ時間と出力時間の余裕を取る。比較実験は固定シードと固定試行回数にすると途中の改善を再現しやすい。本番の経過時間制御は別に測る。

### 例題

```python
rng = Random(7)
values = [rng.randrange(100) for _ in range(3)]
assert values == [41,19,50]
assert run_batches(0, 16, lambda: None) == 0
```

[分野の目次](README.md) · [全体の目次](../README.md)
