# グラフ

経路・連結性・依存関係・流量を扱う。

[全体の目次](../README.md)

| 項目 | 評価 | できること・計算量 |
| --- | :---: | --- |
| [ダイクストラ法 / Dijkstra's Algorithm](dijkstra.md) | 5/5 | 非負重みグラフの単一始点最短距離を O(V+E log(E+1)) で求める。 |
| [グリッド探索 / Grid BFS](grid-bfs.md) | 5/5 | 壁のある H×W マスで上下左右の最短歩数を O(HW) で求める。 |
| [トポロジカルソート・DAG DP / Topological Sort and DAG DP](toposort.md) | 5/5 | 依存関係を守る順序を O(V+E) で求め、有向閉路を検出する。 |
| [幅優先探索・深さ優先探索 / BFS and DFS](traversal.md) | 5/5 | 到達可能頂点や辺数距離を O(V+E) で求める。 |
| [ベルマン–フォード法 / Bellman–Ford Algorithm](bellman-ford.md) | 4/5 | 負辺を含む最短距離と負閉路の影響範囲を O(VE+V) で求める。 |
| [二部グラフ判定 / Bipartite Graph Test](bipartite.md) | 4/5 | 無向グラフを隣同士で色が違う二色に塗れるか O(V+E) で判定する。 |
| [有向閉路の検出・復元 / Directed Cycle Detection and Recovery](cycle.md) | 4/5 | 有向グラフの閉路を一つ O(V+E) で見つけて復元する。 |
| [ワーシャル–フロイド法 / Floyd–Warshall Algorithm](floyd-warshall.md) | 4/5 | 全頂点対の最短距離を O(V³) 時間・O(V²) 空間で求める。 |
| [関数グラフ・閉路と流入木 / Functional Graph](functional.md) | 4/5 | 各頂点が一つの行き先を持つグラフで、閉路の長さと閉路までの距離を O(N) で求める。 |
| [二部マッチング / Hopcroft–Karp Bipartite Matching](matching.md) | 4/5 | 左右の頂点を重複なく最大個数組にする。O((V+E)√V)。 |
| [最大流・最小カット / Maximum Flow and Minimum Cut / Dinic](max-flow.md) | 4/5 | 有向容量つきの最大流と最小カットを求める。一般計算量 O(V²E)。 |
| [最小全域木・クラスカル法 / Minimum Spanning Tree / Kruskal](mst.md) | 4/5 | 全頂点をつなぐ最小費用の森を O(E log E+V) で求める。 |
| [強連結成分分解 / Strongly Connected Components](scc.md) | 4/5 | 互いに行き来できる頂点を O(V+E) でグループ化する。 |
| [0-1 BFS / 0-1 Breadth-First Search](zero-one-bfs.md) | 4/5 | 重みが 0 または 1 のグラフの最短距離を O(V+E) で求める。 |
| [補グラフ BFS / Complement Graph BFS](complement.md) | 3/5 | 列挙された辺が使えないグラフで、使える辺の最短距離を O(V+E) 期待時間で求める。 |
| [辺の追加・削除を伴う連結判定 / Offline Dynamic Connectivity](dynamic-connectivity.md) | 3/5 | 辺の有効期間を分割し、Q 件の操作を O(Q log Q log N) で処理する。 |
| [オイラー路 / Eulerian Trail / Hierholzer](euler-trail.md) | 3/5 | 全ての辺を一度ずつ通る経路を O(V+E) で復元する。 |
| [橋・関節点 / Bridges and Articulation Points / Lowlink](lowlink.md) | 3/5 | 無向グラフの橋と関節点を O(V+E) で求める。多重辺可。 |
| [最小費用流 / Minimum-Cost Flow](min-cost-flow.md) | 3/5 | 指定量まで流す最小費用を求める。最短路探索 K 回で O(K(V+E log(E+1)))。 |
| [ビット集合による到達性 / Bitset Reachability](reachability-bitset.md) | 3/5 | DAG の各頂点からの到達先を逆トポロジカル順のビット OR で求める。 |
| [2-SAT・二択の制約 / 2-Satisfiability](two-sat.md) | 3/5 | 二つのリテラルの OR からなる制約を O(N+M) で解く。 |
