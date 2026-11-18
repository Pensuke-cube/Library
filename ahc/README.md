# AHC

初期解を構築し、限られた時間でスコアを改善する。

[全体の目次](../README.md)

| 項目 | 評価 | できること・計算量 |
| --- | :---: | --- |
| [焼きなまし法 / Simulated Annealing](annealing.md) | 5/5 | 改善に加えて一部の悪化を受理し、局所解から抜け出す。K 回の費用は O(K×近傍評価費用)。 |
| [ビームサーチ / Beam Search](beam.md) | 5/5 | 各深さで上位 B 状態だけ残す。深さ D、分岐 K の選別は O(DBK log(B+1))。 |
| [評価関数・差分検算・ベンチマーク / Scoring, Delta Validation and Benchmarking](evaluation.md) | 5/5 | 採点ロジックを局所で再現し、試行 K 件を O(K×採点費用) で比較する。 |
| [初期解・貪欲構築 / Greedy Construction](greedy.md) | 5/5 | 実行可能な初期解を作る。最近傍で巡回順を作る例は O(N²)。 |
| [山登り法・多点スタート / Hill Climbing and Random Restarts](hill-climb.md) | 5/5 | 近傍を試して改善だけ採用する。K 回の費用は O(K×近傍評価費用)。 |
| [時間管理・乱数の再現 / Time Budget and Reproducibility](time.md) | 5/5 | 実行時間と試行回数を管理する。時刻確認を B 回に一度にまとめる。 |
| [2-opt・巡回路の差分評価 / 2-opt and Incremental Scoring](two-opt.md) | 5/5 | 対称な巡回路の区間反転を O(1) で評価する。採用時の反転は区間長に比例。 |
| [候補リスト・近傍の絞り込み / Candidate Lists and Neighborhood Pruning](candidate-list.md) | 4/5 | 各点で評価する近傍を N 個から K 個に絞る。例の前処理は O(N² log(K+1))。 |
| [大近傍探索・壊して作り直す / Large Neighborhood Search](lns.md) | 4/5 | 解の一部を外して再構築する。K 回の費用はコピー・修復・評価の K 回分。 |
| [可逆な状態更新・ロールバック / Reversible Moves and Rollback](undo.md) | 4/5 | 候補を適用して評価し、変更箇所だけを元に戻す。K 箇所の更新と復元は O(K)。 |
| [Zobrist ハッシュ・状態重複除去 / Zobrist Hashing](zobrist.md) | 4/5 | 局所変更後の状態ハッシュを変更箇所数に比例する時間で更新する。 |
