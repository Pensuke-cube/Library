# AtCoder Python ライブラリ

Python / PyPy で使う競技プログラミングの解説とコード。添字は 0 始まり、区間は原則として半開区間 [l,r)。

**評価**　5 頻出・基礎 ／ 4 頻出の応用 ／ 3 用途が限られる発展

## 分野から探す

- [基本手法](basics/README.md) — 制約から解法を選び、列や区間を処理する。
- [データ構造](structures/README.md) — 更新と質問の種類に応じて、必要な情報を保つ。
- [グラフ](graphs/README.md) — 経路・連結性・依存関係・流量を扱う。
- [木](trees/README.md) — 根付き木として部分木やパスを処理する。
- [動的計画法](dp/README.md) — 状態と遷移を決め、小さい部分問題から解く。
- [数学・数論](math/README.md) — 整数・剰余・数え上げ・多項式を扱う。
- [文字列](strings/README.md) — 一致・周期・接頭辞・回文を扱う。
- [幾何](geometry/README.md) — 点・線分・多角形を座標で扱う。
- [AHC](ahc/README.md) — 初期解を構築し、限られた時間でスコアを改善する。

## 目的から探す

| やりたいこと | 候補 |
| --- | --- |
| 和・最小値・異なる値の個数を区間ごとに求める | [累積和](basics/prefix.md)・[スパーステーブル](structures/sparse-table.md)・[Mo](structures/sqrt-mo.md) |
| 更新しながら区間を集約する | [Fenwick 木](structures/fenwick.md)・[セグメント木](structures/segment-tree.md)・[遅延セグメント木](structures/lazy-segment-tree.md) |
| 次に小さい値や k 番目を取る | [二分探索](basics/binary-search.md)・[順序付き多重集合](structures/ordered-multiset.md) |
| 最短経路を求める | [BFS](graphs/traversal.md)・[0-1 BFS](graphs/zero-one-bfs.md)・[ダイクストラ法](graphs/dijkstra.md)・[負辺あり](graphs/bellman-ford.md) |
| つながっているか調べる | [Union-Find](structures/dsu.md)・[強連結成分](graphs/scc.md)・[辺の削除あり](graphs/dynamic-connectivity.md) |
| 木の部分木やパスを取り出す | [オイラーツアー](trees/euler-tour.md)・[LCA](trees/lca.md)・[重軽分解](trees/hld.md) |
| 選んだ要素の和を管理する | [ナップサック](dp/knapsack.md)・[ビット集合](dp/subset-sum.md)・[半分全列挙](basics/meet-in-middle.md) |
| 文字列の一致を調べる | [KMP](strings/kmp.md)・[Z アルゴリズム](strings/z.md)・[ローリングハッシュ](strings/rolling-hash.md) |
| 制限時間内にスコアを伸ばす | [山登り](ahc/hill-climb.md)・[焼きなまし](ahc/annealing.md)・[ビームサーチ](ahc/beam.md) |

## 全項目

### 基本手法

| 項目 | 評価 | できること・計算量 |
| --- | :---: | --- |
| [二分探索・答えで二分探索 / Binary Search](basics/binary-search.md) | 5/5 | 整列済み配列の境界や単調な判定が切り替わる点を O(log N) 回で探す。 |
| [計算量と制約 / Complexity and Constraints](basics/complexity.md) | 5/5 | 入力サイズから候補解法の時間・空間使用量を見積もる。 |
| [座標圧縮 / Coordinate Compression](basics/compression.md) | 5/5 | 値の順序を保って 0 からの連番に変換する。O(N log N)。 |
| [全探索・順列・組合せ / Enumeration, Permutations and Combinations](basics/enumerate.md) | 5/5 | 2^N 個の部分集合、N! 個の順列、二項係数個の組合せを列挙する。 |
| [辞書・集合・度数集計 / Dictionary, Set and Frequency Counting](basics/frequency.md) | 5/5 | 所属判定、重複除去、度数集計を平均 O(N) で行う。 |
| [貪欲法・区間スケジューリング / Greedy / Interval Scheduling](basics/greedy.md) | 5/5 | 終了時刻順の貪欲法で共通部分を持たない半開区間を最大個数選ぶ。O(N log N)。 |
| [いもす法・二次元いもす法 / Difference Array / Imos Method](basics/imos.md) | 5/5 | Q 回の区間・長方形加算を記録し、全点を O(N+Q) または O(HW+Q) で復元する。 |
| [標準入出力 / Fast I/O](basics/io.md) | 5/5 | 入力全体を O(B) で読み込み、行ごとの整数配列や出力文字列を扱う。 |
| [累積和・二次元累積和 / Prefix Sums](basics/prefix.md) | 5/5 | 前処理 O(N) または O(HW) の後、区間和や長方形和を O(1) で求める。 |
| [ソートと順序付け / Sorting and Ordering](basics/sort.md) | 5/5 | 要素をキー順に整列する。比較ソート O(N log N)、計数ソート O(N+K)。 |
| [しゃくとり法 / Two Pointers / Sliding Window](basics/two-pointers.md) | 5/5 | 両端が単調に進む区間条件を走査する。追加・削除が O(1) なら全体 O(N)。 |
| [バックトラック・枝刈り / Backtracking and Pruning](basics/backtracking.md) | 4/5 | 候補木を探索し、完成できない枝を早期に除く。最悪計算量は探索木に依存。 |
| [ビット演算・部分マスク列挙 / Bit Operations and Submasks](basics/bit.md) | 4/5 | 集合を整数で表し、立っているビットや 2^k 個の部分集合を列挙する。 |
| [構築・不変量 / Constructive Algorithms and Invariants](basics/constructive.md) | 4/5 | 達成条件を式に直して実例を作る。例は N 個の整数を O(N) で構築。 |
| [半分全列挙 / Meet in the Middle](basics/meet-in-middle.md) | 4/5 | 部分集合問題を二分し、O(N·2^(N/2)) 時間と O(2^(N/2)) 空間で合成する。 |
| [置換・順列の巡回分解 / Permutation and Cycle Decomposition](basics/permutation.md) | 4/5 | 置換を O(N) で周期に分解し、K 回先をまとめて求める。 |
| [シミュレーション・周期検出 / Simulation and Cycle Detection](basics/simulation.md) | 4/5 | 決定的な遷移の T 回後を、出現した状態数までの計算で求める。 |
| [イベント処理・スイープライン / Sweep Line](basics/sweep.md) | 4/5 | 座標のイベントだけを O(N log N) で走査し、区間の重なりや被覆長を求める。 |
| [単峰探索 / Unimodal Search](basics/unimodal.md) | 3/5 | 離散凸関数の最小位置を O(log N) 回の評価で探す。 |

### データ構造

| 項目 | 評価 | できること・計算量 |
| --- | :---: | --- |
| [素集合データ構造・Union-Find / Disjoint Set Union](structures/dsu.md) | 5/5 | 併合・同じ連結成分かの判定を償却 O(α(N)) で行う。 |
| [Fenwick 木・転倒数 / Fenwick Tree / Binary Indexed Tree](structures/fenwick.md) | 5/5 | 一点加算・区間和・累積和の境界探索を O(log N) で行う。 |
| [優先度付きキュー・遅延削除 / Priority Queue and Lazy Deletion](structures/heap.md) | 5/5 | 最小値を O(1) で参照し、追加・取り出しを O(log N) で行う。 |
| [遅延セグメント木 / Lazy Segment Tree](structures/lazy-segment-tree.md) | 5/5 | 区間更新と区間集約を O(log N) で行う。 |
| [セグメント木 / Segment Tree](structures/segment-tree.md) | 5/5 | 一点代入・区間集約・区間の右境界探索を O(log N) で行う。 |
| [スタック・キュー・両端キュー / Stack, Queue and Deque](structures/stack-queue.md) | 5/5 | 末尾や先頭への追加・取り出しを O(1) で行う。 |
| [ダブリング / Binary Lifting / Doubling](structures/doubling.md) | 4/5 | 決定的な遷移の K 回先を、前処理 O(N log K) 後に O(log K) で求める。 |
| [連続区間の管理・区間の併合 / Interval Set and Interval Merging](structures/interval-map.md) | 4/5 | 半開区間の和集合を重複しない区間の列にまとめる。O(N log N)。 |
| [最小除外値・動的 MEX / Minimum Excluded Value / MEX](structures/mex.md) | 4/5 | 一点置換と最小の未出非負整数の照会を合わせて Q 回を O(N+Q log(N+1)) で処理する。 |
| [単調キュー・単調スタック / Monotonic Queue and Stack](structures/monotonic.md) | 4/5 | 全固定幅区間の最小値や各要素の直前の小さい要素を O(N) で求める。 |
| [オフラインクエリ・ソートで処理 / Offline Query Processing](structures/offline.md) | 4/5 | クエリを並べ替えて共有部分を使い、値の閾値つき区間件数を O((N+Q)log(N+Q)) で求める。 |
| [順序付き多重集合 / Ordered Multiset](structures/ordered-multiset.md) | 4/5 | 既知の値域で追加・削除・順位・k 番目を O(log M) で処理する。 |
| [スパーステーブル / Sparse Table](structures/sparse-table.md) | 4/5 | 変更のない列を O(N log N) で前処理し、区間最小・最大・GCD を O(1) で求める。 |
| [区間加算・区間和の専用 Fenwick 木 / Range Add and Range Sum with Two Fenwick Trees](structures/specialized-range.md) | 4/5 | 区間加算と区間和を O(log N) で行う。集約・作用のコールバックを使わない。 |
| [スライド区間集約 / Sliding Window Aggregation / SWAG](structures/swag.md) | 4/5 | 末尾追加・先頭削除を償却 O(1)、区間全体の集約を O(1) で行う。 |
| [中央値・上下二つのヒープ / Running Median with Two Heaps](structures/two-heaps.md) | 4/5 | 数を O(log N) で追加し、下側中央値を O(1) で求める。 |
| [重み付き Union-Find / Potentialized Union-Find](structures/weighted-dsu.md) | 4/5 | 差分制約 x[b]-x[a]=w の追加と照会を償却 O(α(N)) で行う。 |
| [二進トライ・XOR 最小値 / Binary Trie and Minimum XOR](structures/bit-trie.md) | 3/5 | 非負整数を追加し、指定値との XOR の最小値を O(B) で求める。 |
| [直線最小値・Li Chao 木 / Li Chao Tree](structures/li-chao.md) | 3/5 | 直線を追加し、既知の x における最小値を各 O(log N) で求める。 |
| [マージソート木・静的区間順位 / Merge Sort Tree](structures/merge-sort-tree.md) | 3/5 | 静的な区間内の閾値以下の個数を O(log² N) で求める。構築 O(N log N)。 |
| [巻き戻し Union-Find・動的連結性 / Rollback DSU and Offline Dynamic Connectivity](structures/rollback-dsu.md) | 3/5 | 連結成分の結合・判定を O(log N)、一回の結合の巻き戻しを O(1) で行う。 |
| [平方分割・Mo のアルゴリズム / Square-Root Decomposition and Mo's Algorithm](structures/sqrt-mo.md) | 3/5 | 静的な区間クエリを O(Q log Q+(N+Q)√N) の目安で処理する。 |

### グラフ

| 項目 | 評価 | できること・計算量 |
| --- | :---: | --- |
| [ダイクストラ法 / Dijkstra's Algorithm](graphs/dijkstra.md) | 5/5 | 非負重みグラフの単一始点最短距離を O(V+E log(E+1)) で求める。 |
| [グリッド探索 / Grid BFS](graphs/grid-bfs.md) | 5/5 | 壁のある H×W マスで上下左右の最短歩数を O(HW) で求める。 |
| [トポロジカルソート・DAG DP / Topological Sort and DAG DP](graphs/toposort.md) | 5/5 | 依存関係を守る順序を O(V+E) で求め、有向閉路を検出する。 |
| [幅優先探索・深さ優先探索 / BFS and DFS](graphs/traversal.md) | 5/5 | 到達可能頂点や辺数距離を O(V+E) で求める。 |
| [ベルマン–フォード法 / Bellman–Ford Algorithm](graphs/bellman-ford.md) | 4/5 | 負辺を含む最短距離と負閉路の影響範囲を O(VE+V) で求める。 |
| [二部グラフ判定 / Bipartite Graph Test](graphs/bipartite.md) | 4/5 | 無向グラフを隣同士で色が違う二色に塗れるか O(V+E) で判定する。 |
| [有向閉路の検出・復元 / Directed Cycle Detection and Recovery](graphs/cycle.md) | 4/5 | 有向グラフの閉路を一つ O(V+E) で見つけて復元する。 |
| [ワーシャル–フロイド法 / Floyd–Warshall Algorithm](graphs/floyd-warshall.md) | 4/5 | 全頂点対の最短距離を O(V³) 時間・O(V²) 空間で求める。 |
| [関数グラフ・閉路と流入木 / Functional Graph](graphs/functional.md) | 4/5 | 各頂点が一つの行き先を持つグラフで、閉路の長さと閉路までの距離を O(N) で求める。 |
| [二部マッチング / Hopcroft–Karp Bipartite Matching](graphs/matching.md) | 4/5 | 左右の頂点を重複なく最大個数組にする。O((V+E)√V)。 |
| [最大流・最小カット / Maximum Flow and Minimum Cut / Dinic](graphs/max-flow.md) | 4/5 | 有向容量つきの最大流と最小カットを求める。一般計算量 O(V²E)。 |
| [最小全域木・クラスカル法 / Minimum Spanning Tree / Kruskal](graphs/mst.md) | 4/5 | 全頂点をつなぐ最小費用の森を O(E log E+V) で求める。 |
| [強連結成分分解 / Strongly Connected Components](graphs/scc.md) | 4/5 | 互いに行き来できる頂点を O(V+E) でグループ化する。 |
| [0-1 BFS / 0-1 Breadth-First Search](graphs/zero-one-bfs.md) | 4/5 | 重みが 0 または 1 のグラフの最短距離を O(V+E) で求める。 |
| [補グラフ BFS / Complement Graph BFS](graphs/complement.md) | 3/5 | 列挙された辺が使えないグラフで、使える辺の最短距離を O(V+E) 期待時間で求める。 |
| [辺の追加・削除を伴う連結判定 / Offline Dynamic Connectivity](graphs/dynamic-connectivity.md) | 3/5 | 辺の有効期間を分割し、Q 件の操作を O(Q log Q log N) で処理する。 |
| [オイラー路 / Eulerian Trail / Hierholzer](graphs/euler-trail.md) | 3/5 | 全ての辺を一度ずつ通る経路を O(V+E) で復元する。 |
| [橋・関節点 / Bridges and Articulation Points / Lowlink](graphs/lowlink.md) | 3/5 | 無向グラフの橋と関節点を O(V+E) で求める。多重辺可。 |
| [最小費用流 / Minimum-Cost Flow](graphs/min-cost-flow.md) | 3/5 | 指定量まで流す最小費用を求める。最短路探索 K 回で O(K(V+E log(E+1)))。 |
| [ビット集合による到達性 / Bitset Reachability](graphs/reachability-bitset.md) | 3/5 | DAG の各頂点からの到達先を逆トポロジカル順のビット OR で求める。 |
| [2-SAT・二択の制約 / 2-Satisfiability](graphs/two-sat.md) | 3/5 | 二つのリテラルの OR からなる制約を O(N+M) で解く。 |

### 木

| 項目 | 評価 | できること・計算量 |
| --- | :---: | --- |
| [木の根付き化・オイラーツアー / Rooting and Euler Tour](trees/euler-tour.md) | 5/5 | 部分木を連続区間に変換する。前処理 O(N)、区間取得 O(1)。 |
| [木 DP / Tree Dynamic Programming](trees/tree-dp.md) | 5/5 | 子から親への集約で木の独立集合などを求める。例は O(N)。 |
| [木の直径 / Tree Diameter](trees/diameter.md) | 4/5 | 非負重みの木で最も離れた二頂点と距離を O(N) で求める。 |
| [最小共通祖先・木の距離 / Lowest Common Ancestor](trees/lca.md) | 4/5 | 前処理 O(N log N)、LCA・距離を O(log N) で求める。 |
| [全方位木 DP / Rerooting DP](trees/reroot.md) | 4/5 | 全ての頂点を根とした答えを O(N) でまとめて求める。 |
| [木の重心・重心分解 / Tree Centroid and Centroid Decomposition](trees/centroid.md) | 3/5 | 残る連結成分が全て半分以下になる頂点で木を再帰分割する。O(N log N)。 |
| [重軽分解 / Heavy-Light Decomposition](trees/hld.md) | 3/5 | 木のパスを O(log N) 個の連続区間に分解する。構築 O(N)。 |

### 動的計画法

| 項目 | 評価 | できること・計算量 |
| --- | :---: | --- |
| [グリッド DP / Grid DP](dp/grid.md) | 5/5 | 右・下に進む経路数を O(HW) 時間・O(W) 空間で求める。 |
| [ナップサック DP / Knapsack DP](dp/knapsack.md) | 5/5 | 各品物を高々一度選んで容量 W 以下で価値を最大化する。O(NW)。 |
| [動的計画法・状態設計 / Dynamic Programming](dp/linear.md) | 5/5 | 小さい部分問題から順に答えを求める。基本の計算量は状態数×遷移数。 |
| [最長増加部分列 / Longest Increasing Subsequence](dp/lis.md) | 5/5 | 狭義増加部分列の最大長を O(N log N) で求める。 |
| [ビット DP・巡回セールスマン / Bitmask DP / Traveling Salesman](dp/bitmask.md) | 4/5 | 訪問集合を状態にして巡回路の最小費用を O(N²2^N) で求める。 |
| [桁 DP / Digit DP](dp/digit.md) | 4/5 | 上限以下の整数を上位桁から数える。O(桁数×状態数×基数)。 |
| [ゲーム DP・Grundy 数 / Game DP and Sprague–Grundy Numbers](dp/game.md) | 4/5 | 手詰まりで負ける公平な有限ゲームを DAG の状態と遷移に比例する時間で解く。 |
| [区間 DP / Interval DP](dp/interval.md) | 4/5 | 区間内の分割や消去を短い区間から解く。全分割を試す例は O(N³)。 |
| [最長共通部分列・編集距離 / LCS and Edit Distance](dp/lcs.md) | 4/5 | 二列の最長共通部分列長と編集距離をそれぞれ O(NM) で求める。 |
| [累積和で DP の遷移を高速化 / Prefix-Sum DP Optimization](dp/prefix-transitions.md) | 4/5 | 直前の状態の連続範囲の和を O(1) で取り、配分数を O(NK) で求める。 |
| [確率・期待値 DP / Probability and Expectation DP](dp/probability.md) | 4/5 | 状態ごとの確率や期待値を遷移式で集約する。例は O(N²)。 |
| [部分和のビット集合 DP / Subset Sum Bitset DP](dp/subset-sum.md) | 4/5 | 非負整数の部分和の到達可否をシフトと OR で一括更新する。 |
| [ビット並列 LCS / Bit-Parallel LCS](dp/lcs-bit.md) | 3/5 | 最長共通部分列長を各文字につき巨大整数演算数回で求める。 |
| [単調性を使う DP 最適化 / Dynamic Programming Optimization](dp/optimizations.md) | 3/5 | 単調な最良分割点を使い、一行の分割 DP を O(N log N) で更新する。 |
| [部分集合ゼータ・メビウス変換 / Subset Zeta and Möbius Transform](dp/sos.md) | 3/5 | 全マスクについて部分マスクの和をまとめる。O(N2^N)。 |

### 数学・数論

| 項目 | 評価 | できること・計算量 |
| --- | :---: | --- |
| [組合せ・階乗・二項係数 / Combinatorics and Binomial Coefficients](math/combinations.md) | 5/5 | 素数法で階乗を前処理し、二項係数・順列数を O(1) で答える。 |
| [切り上げ・等差数列・整数平方根 / Integer Division and Arithmetic Progressions](math/division.md) | 5/5 | 整数だけで商の丸め、等差数列の和、平方根の切り捨てを求める。 |
| [約数列挙・素因数分解・最小素因数 / Divisors, Factorization and Smallest Prime Factor](math/factors.md) | 5/5 | 単発を O(√N) で処理し、最小素因数表があれば分解を O(log N) 回の除算で行う。 |
| [最大公約数・最小公倍数・拡張 Euclid / GCD, LCM and Extended Euclidean Algorithm](math/gcd.md) | 5/5 | 整数の GCD・LCM・Bézout 係数を O(log(min( |
| [剰余・繰り返し二乗法・逆元 / Modular Arithmetic, Binary Exponentiation and Inverse](math/modular.md) | 5/5 | 巨大な冪の剰余を O(log K) 回の乗算で求める。逆元は互いに素なとき存在。 |
| [素数判定・エラトステネスの篩 / Primality Test and Sieve of Eratosthenes](math/primes.md) | 5/5 | 単発の素数判定を O(√N)、N 以下の一括判定を O(N log log N) で行う。 |
| [畳み込み・整数パッキング / Convolution and Integer Packing](math/convolution.md) | 4/5 | 積の係数列を整数乗算一回で求める。計算量はパック後の整数乗算に依存。 |
| [中国剰余定理 / Chinese Remainder Theorem](math/crt.md) | 4/5 | 複数の合同式を併合し、最小非負解と周期を求める。 |
| [包除原理・倍数の数え上げ / Inclusion–Exclusion Principle](math/inclusion.md) | 4/5 | 重複する条件の和集合の大きさを O(2^K) 回の共通部分計算で求める。 |
| [行列積・行列累乗 / Matrix Multiplication and Exponentiation](math/matrix.md) | 4/5 | 線形な状態遷移の K 回先を O(D³ log K) で求める。 |
| [床関数の和 / Floor Sum](math/floor-sum.md) | 3/5 | Σ floor((ai+b)/m) を m の対数回の反復で求める。 |
| [ガウス消去・線形基底 / Gaussian Elimination and XOR Basis](math/gaussian.md) | 3/5 | GF(2) の線形独立性や XOR で表せる値を O(NB) 回の整数演算で求める。 |
| [ミラー–ラビン素数判定 / Miller–Rabin Primality Test](math/miller-rabin.md) | 3/5 | 64 ビット非負整数の素数判定を少数回の冪剰余で行う。 |
| [約数・倍数ゼータ変換とメビウス反転 / Divisor and Multiple Zeta / Möbius Transforms](math/multiples-transform.md) | 3/5 | 1〜N の約数和・倍数和を O(N log log N) で求め、逆変換も同じ時間。 |
| [数論変換・高速畳み込み / Number-Theoretic Transform / NTT](math/ntt.md) | 3/5 | 998244353 を法とする畳み込みを O(L log L) で求める。 |
| [ポラードのρ法・64 ビット素因数分解 / Pollard's Rho Factorization](math/pollard-rho.md) | 3/5 | 64 ビット整数を素因数分解する。素因数 p の発見は O(√p) 回の反復が目安。 |

### 文字列

| 項目 | 評価 | できること・計算量 |
| --- | :---: | --- |
| [文字列・文字コード・回文 / String Operations and Palindromes](strings/basics.md) | 5/5 | 文字列の切り出し・反転や連続区間の判定を行う。反転は O(N)。 |
| [ランレングス圧縮 / Run-Length Encoding](strings/rle.md) | 5/5 | 同じ値が連続する区間を (値,長さ) にする。O(N)。 |
| [KMP 法・文字列の周期 / Knuth–Morris–Pratt Algorithm](strings/kmp.md) | 4/5 | パターンの全出現位置と接頭辞の境界を O(N+M) で求める。 |
| [ローリングハッシュ / Rolling Hash](strings/rolling-hash.md) | 4/5 | 前処理 O(N) で任意の部分文字列を O(1) でハッシュ化する。 |
| [トライ木・接頭辞の個数 / Trie](strings/trie.md) | 4/5 | 文字列を長さに比例する時間で追加し、接頭辞に一致する個数を求める。 |
| [Z アルゴリズム / Z Algorithm](strings/z.md) | 4/5 | 全位置からの接尾辞と先頭の最長共通接頭辞を O(N) で求める。 |
| [複数パターン検索 / Aho–Corasick Automaton](strings/aho-corasick.md) | 3/5 | パターン総長 P のトライを使って複数パターンの出現を一度の走査で数える。 |
| [回文半径・Manacher 法 / Manacher's Algorithm](strings/manacher.md) | 3/5 | 奇数長・偶数長回文の最大半径を全中心について O(N) で求める。 |
| [接尾辞配列・LCP 配列 / Suffix Array and LCP Array](strings/suffix-array.md) | 3/5 | 接尾辞の辞書順を O(N log² N)、隣接接尾辞の共通接頭辞長を O(N) で求める。 |

### 幾何

| 項目 | 評価 | できること・計算量 |
| --- | :---: | --- |
| [距離・マンハッタン距離 / Distance and Manhattan Distance](geometry/distance.md) | 4/5 | 二点距離を O(1)、全点対の最大マンハッタン距離を O(N) で求める。 |
| [外積・線分交差 / Cross Product and Segment Intersection](geometry/orientation.md) | 4/5 | 整数座標で回転方向や端点を含む線分交差を O(1) 回の演算で判定する。 |
| [偏角順ソート / Polar Angle Sorting](geometry/angle.md) | 3/5 | 原点以外の整数ベクトルを偏角順に O(N log N) で並べる。 |
| [多角形の面積 / Polygon Area / Shoelace Formula](geometry/area.md) | 3/5 | 巡回順の頂点から符号付き面積の二倍を O(N) で求める。 |
| [円の位置関係・距離比較 / Circle Relations](geometry/circle.md) | 3/5 | 二円が交わるか、接するか、一方が内側かを O(1) 回の整数演算で判定する。 |
| [凸包 / Convex Hull / Monotone Chain](geometry/hull.md) | 3/5 | 点群を囲む最小の凸多角形を O(N log N) で求める。 |
| [長方形の和集合面積 / Area of a Union of Rectangles](geometry/rect-union.md) | 3/5 | 軸平行な長方形 N 個の和集合の面積を O(N log N) で求める。 |

### AHC

| 項目 | 評価 | できること・計算量 |
| --- | :---: | --- |
| [焼きなまし法 / Simulated Annealing](ahc/annealing.md) | 5/5 | 改善に加えて一部の悪化を受理し、局所解から抜け出す。K 回の費用は O(K×近傍評価費用)。 |
| [ビームサーチ / Beam Search](ahc/beam.md) | 5/5 | 各深さで上位 B 状態だけ残す。深さ D、分岐 K の選別は O(DBK log(B+1))。 |
| [評価関数・差分検算・ベンチマーク / Scoring, Delta Validation and Benchmarking](ahc/evaluation.md) | 5/5 | 採点ロジックを局所で再現し、試行 K 件を O(K×採点費用) で比較する。 |
| [初期解・貪欲構築 / Greedy Construction](ahc/greedy.md) | 5/5 | 実行可能な初期解を作る。最近傍で巡回順を作る例は O(N²)。 |
| [山登り法・多点スタート / Hill Climbing and Random Restarts](ahc/hill-climb.md) | 5/5 | 近傍を試して改善だけ採用する。K 回の費用は O(K×近傍評価費用)。 |
| [時間管理・乱数の再現 / Time Budget and Reproducibility](ahc/time.md) | 5/5 | 実行時間と試行回数を管理する。時刻確認を B 回に一度にまとめる。 |
| [2-opt・巡回路の差分評価 / 2-opt and Incremental Scoring](ahc/two-opt.md) | 5/5 | 対称な巡回路の区間反転を O(1) で評価する。採用時の反転は区間長に比例。 |
| [候補リスト・近傍の絞り込み / Candidate Lists and Neighborhood Pruning](ahc/candidate-list.md) | 4/5 | 各点で評価する近傍を N 個から K 個に絞る。例の前処理は O(N² log(K+1))。 |
| [大近傍探索・壊して作り直す / Large Neighborhood Search](ahc/lns.md) | 4/5 | 解の一部を外して再構築する。K 回の費用はコピー・修復・評価の K 回分。 |
| [可逆な状態更新・ロールバック / Reversible Moves and Rollback](ahc/undo.md) | 4/5 | 候補を適用して評価し、変更箇所だけを元に戻す。K 箇所の更新と復元は O(K)。 |
| [Zobrist ハッシュ・状態重複除去 / Zobrist Hashing](ahc/zobrist.md) | 4/5 | 局所変更後の状態ハッシュを変更箇所数に比例する時間で更新する。 |
