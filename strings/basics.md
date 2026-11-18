# 文字列・文字コード・回文 / String Operations and Palindromes

**5/5** · 文字列の切り出し・反転や連続区間の判定を行う。反転は O(N)。

## 使い方

is_palindrome(s) は列全体が回文か。連結が多いときは "".join(parts)。

## コード

```python
def is_palindrome(s):
    return s == s[::-1]
```

## 考え方

str は文字、bytes はバイト。bytes の添字アクセスは整数になる。長い文字列に一文字ずつ += する処理はコピーで二乗時間になり得るので、リストに貯める。英小文字の添字は ord(c)-ord("a")。

### 例題

```python
assert is_palindrome("level") and not is_palindrome("abc")
assert "".join(["ab", "c"]) == "abc"
```

[分野の目次](README.md) · [全体の目次](../README.md)
