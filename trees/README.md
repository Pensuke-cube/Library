# 木

根付き木として部分木やパスを処理する。

[全体の目次](../README.md)

| 項目 | 評価 | できること・計算量 |
| --- | :---: | --- |
| [木の根付き化・オイラーツアー / Rooting and Euler Tour](euler-tour.md) | 5/5 | 部分木を連続区間に変換する。前処理 O(N)、区間取得 O(1)。 |
| [木 DP / Tree Dynamic Programming](tree-dp.md) | 5/5 | 子から親への集約で木の独立集合などを求める。例は O(N)。 |
| [木の直径 / Tree Diameter](diameter.md) | 4/5 | 非負重みの木で最も離れた二頂点と距離を O(N) で求める。 |
| [最小共通祖先・木の距離 / Lowest Common Ancestor](lca.md) | 4/5 | 前処理 O(N log N)、LCA・距離を O(log N) で求める。 |
| [全方位木 DP / Rerooting DP](reroot.md) | 4/5 | 全ての頂点を根とした答えを O(N) でまとめて求める。 |
| [木の重心・重心分解 / Tree Centroid and Centroid Decomposition](centroid.md) | 3/5 | 残る連結成分が全て半分以下になる頂点で木を再帰分割する。O(N log N)。 |
| [重軽分解 / Heavy-Light Decomposition](hld.md) | 3/5 | 木のパスを O(log N) 個の連続区間に分解する。構築 O(N)。 |
