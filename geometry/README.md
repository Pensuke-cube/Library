# 幾何

点・線分・多角形を座標で扱う。

[全体の目次](../README.md)

| 項目 | 評価 | できること・計算量 |
| --- | :---: | --- |
| [距離・マンハッタン距離 / Distance and Manhattan Distance](distance.md) | 4/5 | 二点距離を O(1)、全点対の最大マンハッタン距離を O(N) で求める。 |
| [外積・線分交差 / Cross Product and Segment Intersection](orientation.md) | 4/5 | 整数座標で回転方向や端点を含む線分交差を O(1) 回の演算で判定する。 |
| [偏角順ソート / Polar Angle Sorting](angle.md) | 3/5 | 原点以外の整数ベクトルを偏角順に O(N log N) で並べる。 |
| [多角形の面積 / Polygon Area / Shoelace Formula](area.md) | 3/5 | 巡回順の頂点から符号付き面積の二倍を O(N) で求める。 |
| [円の位置関係・距離比較 / Circle Relations](circle.md) | 3/5 | 二円が交わるか、接するか、一方が内側かを O(1) 回の整数演算で判定する。 |
| [凸包 / Convex Hull / Monotone Chain](hull.md) | 3/5 | 点群を囲む最小の凸多角形を O(N log N) で求める。 |
| [長方形の和集合面積 / Area of a Union of Rectangles](rect-union.md) | 3/5 | 軸平行な長方形 N 個の和集合の面積を O(N log N) で求める。 |
