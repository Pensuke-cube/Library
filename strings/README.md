# 文字列

一致・周期・接頭辞・回文を扱う。

[全体の目次](../README.md)

| 項目 | 評価 | できること・計算量 |
| --- | :---: | --- |
| [文字列・文字コード・回文 / String Operations and Palindromes](basics.md) | 5/5 | 文字列の切り出し・反転や連続区間の判定を行う。反転は O(N)。 |
| [ランレングス圧縮 / Run-Length Encoding](rle.md) | 5/5 | 同じ値が連続する区間を (値,長さ) にする。O(N)。 |
| [KMP 法・文字列の周期 / Knuth–Morris–Pratt Algorithm](kmp.md) | 4/5 | パターンの全出現位置と接頭辞の境界を O(N+M) で求める。 |
| [ローリングハッシュ / Rolling Hash](rolling-hash.md) | 4/5 | 前処理 O(N) で任意の部分文字列を O(1) でハッシュ化する。 |
| [トライ木・接頭辞の個数 / Trie](trie.md) | 4/5 | 文字列を長さに比例する時間で追加し、接頭辞に一致する個数を求める。 |
| [Z アルゴリズム / Z Algorithm](z.md) | 4/5 | 全位置からの接尾辞と先頭の最長共通接頭辞を O(N) で求める。 |
| [複数パターン検索 / Aho–Corasick Automaton](aho-corasick.md) | 3/5 | パターン総長 P のトライを使って複数パターンの出現を一度の走査で数える。 |
| [回文半径・Manacher 法 / Manacher's Algorithm](manacher.md) | 3/5 | 奇数長・偶数長回文の最大半径を全中心について O(N) で求める。 |
| [接尾辞配列・LCP 配列 / Suffix Array and LCP Array](suffix-array.md) | 3/5 | 接尾辞の辞書順を O(N log² N)、隣接接尾辞の共通接頭辞長を O(N) で求める。 |
