# 基本手法

制約から解法を選び、列や区間を処理する。

[全体の目次](../README.md)

| 項目 | 評価 | できること・計算量 |
| --- | :---: | --- |
| [二分探索・答えで二分探索 / Binary Search](binary-search.md) | 5/5 | 整列済み配列の境界や単調な判定が切り替わる点を O(log N) 回で探す。 |
| [計算量と制約 / Complexity and Constraints](complexity.md) | 5/5 | 入力サイズから候補解法の時間・空間使用量を見積もる。 |
| [座標圧縮 / Coordinate Compression](compression.md) | 5/5 | 値の順序を保って 0 からの連番に変換する。O(N log N)。 |
| [全探索・順列・組合せ / Enumeration, Permutations and Combinations](enumerate.md) | 5/5 | 2^N 個の部分集合、N! 個の順列、二項係数個の組合せを列挙する。 |
| [辞書・集合・度数集計 / Dictionary, Set and Frequency Counting](frequency.md) | 5/5 | 所属判定、重複除去、度数集計を平均 O(N) で行う。 |
| [貪欲法・区間スケジューリング / Greedy / Interval Scheduling](greedy.md) | 5/5 | 終了時刻順の貪欲法で共通部分を持たない半開区間を最大個数選ぶ。O(N log N)。 |
| [いもす法・二次元いもす法 / Difference Array / Imos Method](imos.md) | 5/5 | Q 回の区間・長方形加算を記録し、全点を O(N+Q) または O(HW+Q) で復元する。 |
| [標準入出力 / Fast I/O](io.md) | 5/5 | 入力全体を O(B) で読み込み、行ごとの整数配列や出力文字列を扱う。 |
| [累積和・二次元累積和 / Prefix Sums](prefix.md) | 5/5 | 前処理 O(N) または O(HW) の後、区間和や長方形和を O(1) で求める。 |
| [ソートと順序付け / Sorting and Ordering](sort.md) | 5/5 | 要素をキー順に整列する。比較ソート O(N log N)、計数ソート O(N+K)。 |
| [しゃくとり法 / Two Pointers / Sliding Window](two-pointers.md) | 5/5 | 両端が単調に進む区間条件を走査する。追加・削除が O(1) なら全体 O(N)。 |
| [バックトラック・枝刈り / Backtracking and Pruning](backtracking.md) | 4/5 | 候補木を探索し、完成できない枝を早期に除く。最悪計算量は探索木に依存。 |
| [ビット演算・部分マスク列挙 / Bit Operations and Submasks](bit.md) | 4/5 | 集合を整数で表し、立っているビットや 2^k 個の部分集合を列挙する。 |
| [構築・不変量 / Constructive Algorithms and Invariants](constructive.md) | 4/5 | 達成条件を式に直して実例を作る。例は N 個の整数を O(N) で構築。 |
| [半分全列挙 / Meet in the Middle](meet-in-middle.md) | 4/5 | 部分集合問題を二分し、O(N·2^(N/2)) 時間と O(2^(N/2)) 空間で合成する。 |
| [置換・順列の巡回分解 / Permutation and Cycle Decomposition](permutation.md) | 4/5 | 置換を O(N) で周期に分解し、K 回先をまとめて求める。 |
| [シミュレーション・周期検出 / Simulation and Cycle Detection](simulation.md) | 4/5 | 決定的な遷移の T 回後を、出現した状態数までの計算で求める。 |
| [イベント処理・スイープライン / Sweep Line](sweep.md) | 4/5 | 座標のイベントだけを O(N log N) で走査し、区間の重なりや被覆長を求める。 |
| [単峰探索 / Unimodal Search](unimodal.md) | 3/5 | 離散凸関数の最小位置を O(log N) 回の評価で探す。 |
