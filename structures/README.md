# データ構造

更新と質問の種類に応じて、必要な情報を保つ。

[全体の目次](../README.md)

| 項目 | 評価 | できること・計算量 |
| --- | :---: | --- |
| [素集合データ構造・Union-Find / Disjoint Set Union](dsu.md) | 5/5 | 併合・同じ連結成分かの判定を償却 O(α(N)) で行う。 |
| [Fenwick 木・転倒数 / Fenwick Tree / Binary Indexed Tree](fenwick.md) | 5/5 | 一点加算・区間和・累積和の境界探索を O(log N) で行う。 |
| [優先度付きキュー・遅延削除 / Priority Queue and Lazy Deletion](heap.md) | 5/5 | 最小値を O(1) で参照し、追加・取り出しを O(log N) で行う。 |
| [遅延セグメント木 / Lazy Segment Tree](lazy-segment-tree.md) | 5/5 | 区間更新と区間集約を O(log N) で行う。 |
| [セグメント木 / Segment Tree](segment-tree.md) | 5/5 | 一点代入・区間集約・区間の右境界探索を O(log N) で行う。 |
| [スタック・キュー・両端キュー / Stack, Queue and Deque](stack-queue.md) | 5/5 | 末尾や先頭への追加・取り出しを O(1) で行う。 |
| [ダブリング / Binary Lifting / Doubling](doubling.md) | 4/5 | 決定的な遷移の K 回先を、前処理 O(N log K) 後に O(log K) で求める。 |
| [連続区間の管理・区間の併合 / Interval Set and Interval Merging](interval-map.md) | 4/5 | 半開区間の和集合を重複しない区間の列にまとめる。O(N log N)。 |
| [最小除外値・動的 MEX / Minimum Excluded Value / MEX](mex.md) | 4/5 | 一点置換と最小の未出非負整数の照会を合わせて Q 回を O(N+Q log(N+1)) で処理する。 |
| [単調キュー・単調スタック / Monotonic Queue and Stack](monotonic.md) | 4/5 | 全固定幅区間の最小値や各要素の直前の小さい要素を O(N) で求める。 |
| [オフラインクエリ・ソートで処理 / Offline Query Processing](offline.md) | 4/5 | クエリを並べ替えて共有部分を使い、値の閾値つき区間件数を O((N+Q)log(N+Q)) で求める。 |
| [順序付き多重集合 / Ordered Multiset](ordered-multiset.md) | 4/5 | 既知の値域で追加・削除・順位・k 番目を O(log M) で処理する。 |
| [スパーステーブル / Sparse Table](sparse-table.md) | 4/5 | 変更のない列を O(N log N) で前処理し、区間最小・最大・GCD を O(1) で求める。 |
| [区間加算・区間和の専用 Fenwick 木 / Range Add and Range Sum with Two Fenwick Trees](specialized-range.md) | 4/5 | 区間加算と区間和を O(log N) で行う。集約・作用のコールバックを使わない。 |
| [スライド区間集約 / Sliding Window Aggregation / SWAG](swag.md) | 4/5 | 末尾追加・先頭削除を償却 O(1)、区間全体の集約を O(1) で行う。 |
| [中央値・上下二つのヒープ / Running Median with Two Heaps](two-heaps.md) | 4/5 | 数を O(log N) で追加し、下側中央値を O(1) で求める。 |
| [重み付き Union-Find / Potentialized Union-Find](weighted-dsu.md) | 4/5 | 差分制約 x[b]-x[a]=w の追加と照会を償却 O(α(N)) で行う。 |
| [二進トライ・XOR 最小値 / Binary Trie and Minimum XOR](bit-trie.md) | 3/5 | 非負整数を追加し、指定値との XOR の最小値を O(B) で求める。 |
| [直線最小値・Li Chao 木 / Li Chao Tree](li-chao.md) | 3/5 | 直線を追加し、既知の x における最小値を各 O(log N) で求める。 |
| [マージソート木・静的区間順位 / Merge Sort Tree](merge-sort-tree.md) | 3/5 | 静的な区間内の閾値以下の個数を O(log² N) で求める。構築 O(N log N)。 |
| [巻き戻し Union-Find・動的連結性 / Rollback DSU and Offline Dynamic Connectivity](rollback-dsu.md) | 3/5 | 連結成分の結合・判定を O(log N)、一回の結合の巻き戻しを O(1) で行う。 |
| [平方分割・Mo のアルゴリズム / Square-Root Decomposition and Mo's Algorithm](sqrt-mo.md) | 3/5 | 静的な区間クエリを O(Q log Q+(N+Q)√N) の目安で処理する。 |
