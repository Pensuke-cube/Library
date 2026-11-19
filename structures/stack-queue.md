# スタック・キュー・両端キュー / Stack, Queue and Deque

**5/5** · 末尾や先頭への追加・取り出しを O(1) で行う。

## 使い方

- 後から入れた値を先に取り出すスタックは `s = []` で作る。`s.append(x)` で末尾へ追加し、`s.pop()` で末尾を削除して返す。
- 先に入れた値を先に取り出すキューは `q = deque()` で作る。`q.append(x)` で末尾へ追加し、`q.popleft()` で先頭を削除して返す。
- `deque` は `appendleft(x)` で先頭に追加、`pop()` で末尾からも取り出せる。どちらも空のときは取り出さない。

## コード

```python
from collections import deque
```

## 考え方

後入れ先出しは括弧や DFS に、先入れ先出しは BFS に使う。list.pop(0) は残りの要素をずらすので O(N)。

### 例題

```python
def balanced(s):
    stack = []
    for c in s:
        if c == "(":
            stack.append(c)
        elif stack:
            stack.pop()
        else:
            return False
    return not stack

assert balanced("(())") and not balanced(")(")
```

[分野の目次](README.md) · [全体の目次](../README.md)
