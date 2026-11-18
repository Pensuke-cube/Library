# 動的計画法

状態と遷移を決め、小さい部分問題から解く。

[全体の目次](../README.md)

| 項目 | 評価 | できること・計算量 |
| --- | :---: | --- |
| [グリッド DP / Grid DP](grid.md) | 5/5 | 右・下に進む経路数を O(HW) 時間・O(W) 空間で求める。 |
| [ナップサック DP / Knapsack DP](knapsack.md) | 5/5 | 各品物を高々一度選んで容量 W 以下で価値を最大化する。O(NW)。 |
| [動的計画法・状態設計 / Dynamic Programming](linear.md) | 5/5 | 小さい部分問題から順に答えを求める。基本の計算量は状態数×遷移数。 |
| [最長増加部分列 / Longest Increasing Subsequence](lis.md) | 5/5 | 狭義増加部分列の最大長を O(N log N) で求める。 |
| [ビット DP・巡回セールスマン / Bitmask DP / Traveling Salesman](bitmask.md) | 4/5 | 訪問集合を状態にして巡回路の最小費用を O(N²2^N) で求める。 |
| [桁 DP / Digit DP](digit.md) | 4/5 | 上限以下の整数を上位桁から数える。O(桁数×状態数×基数)。 |
| [ゲーム DP・Grundy 数 / Game DP and Sprague–Grundy Numbers](game.md) | 4/5 | 手詰まりで負ける公平な有限ゲームを DAG の状態と遷移に比例する時間で解く。 |
| [区間 DP / Interval DP](interval.md) | 4/5 | 区間内の分割や消去を短い区間から解く。全分割を試す例は O(N³)。 |
| [最長共通部分列・編集距離 / LCS and Edit Distance](lcs.md) | 4/5 | 二列の最長共通部分列長と編集距離をそれぞれ O(NM) で求める。 |
| [累積和で DP の遷移を高速化 / Prefix-Sum DP Optimization](prefix-transitions.md) | 4/5 | 直前の状態の連続範囲の和を O(1) で取り、配分数を O(NK) で求める。 |
| [確率・期待値 DP / Probability and Expectation DP](probability.md) | 4/5 | 状態ごとの確率や期待値を遷移式で集約する。例は O(N²)。 |
| [部分和のビット集合 DP / Subset Sum Bitset DP](subset-sum.md) | 4/5 | 非負整数の部分和の到達可否をシフトと OR で一括更新する。 |
| [ビット並列 LCS / Bit-Parallel LCS](lcs-bit.md) | 3/5 | 最長共通部分列長を各文字につき巨大整数演算数回で求める。 |
| [単調性を使う DP 最適化 / Dynamic Programming Optimization](optimizations.md) | 3/5 | 単調な最良分割点を使い、一行の分割 DP を O(N log N) で更新する。 |
| [部分集合ゼータ・メビウス変換 / Subset Zeta and Möbius Transform](sos.md) | 3/5 | 全マスクについて部分マスクの和をまとめる。O(N2^N)。 |
