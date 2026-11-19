# 標準入出力 / Fast I/O

**5/5** · 入力全体を O(B) で読み込み、行ごとの整数配列や出力文字列を扱う。

## 使い方

- `input()` は標準入力から一行を `bytes` で返す。整数一つなら `int(input())`、一行の整数列なら `list(map(int, input().split()))`。
- `ints()` は残りの標準入力を末尾まで読み、空白区切りの整数を順に返すイテレータ。`it = ints()` として `next(it)` で一つ読む。
- `write_lines(values)` に出力したい値の列を渡す。一つずつ文字列にして一行ずつ出力する。

## コード

```python
import sys

input = sys.stdin.buffer.readline

def ints():
    return map(int, sys.stdin.buffer.read().split())

def write_lines(values):
    sys.stdout.write("".join(f"{x}\n" for x in values))
```

## 考え方

一括読み込みは EOF まで読む。対話問題では行ごとに読み、出力を flush する。bytes の末尾改行は rstrip(b"\r\n") で除く。

### 例題

```python
# 入力が "3\n10 20 30\n" のとき 60 を出力。
tokens = ints()
n = next(tokens)
print(sum(next(tokens) for _ in range(n)))
```

[分野の目次](README.md) · [全体の目次](../README.md)
