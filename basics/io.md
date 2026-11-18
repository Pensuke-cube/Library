# 標準入出力 / Fast I/O

**5/5** · 入力全体を O(B) で読み込み、行ごとの整数配列や出力文字列を扱う。

## 使い方

行単位なら input()、空白区切りのトークンをまとめて読むなら ints()。B は入出力のバイト数。

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
