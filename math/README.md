# 数学・数論

整数・剰余・数え上げ・多項式を扱う。

[全体の目次](../README.md)

| 項目 | 評価 | できること・計算量 |
| --- | :---: | --- |
| [組合せ・階乗・二項係数 / Combinatorics and Binomial Coefficients](combinations.md) | 5/5 | 素数法で階乗を前処理し、二項係数・順列数を O(1) で答える。 |
| [切り上げ・等差数列・整数平方根 / Integer Division and Arithmetic Progressions](division.md) | 5/5 | 整数だけで商の丸め、等差数列の和、平方根の切り捨てを求める。 |
| [約数列挙・素因数分解・最小素因数 / Divisors, Factorization and Smallest Prime Factor](factors.md) | 5/5 | 単発を O(√N) で処理し、最小素因数表があれば分解を O(log N) 回の除算で行う。 |
| [最大公約数・最小公倍数・拡張 Euclid / GCD, LCM and Extended Euclidean Algorithm](gcd.md) | 5/5 | 整数の GCD・LCM・Bézout 係数を O(log(min( |
| [剰余・繰り返し二乗法・逆元 / Modular Arithmetic, Binary Exponentiation and Inverse](modular.md) | 5/5 | 巨大な冪の剰余を O(log K) 回の乗算で求める。逆元は互いに素なとき存在。 |
| [素数判定・エラトステネスの篩 / Primality Test and Sieve of Eratosthenes](primes.md) | 5/5 | 単発の素数判定を O(√N)、N 以下の一括判定を O(N log log N) で行う。 |
| [畳み込み・整数パッキング / Convolution and Integer Packing](convolution.md) | 4/5 | 積の係数列を整数乗算一回で求める。計算量はパック後の整数乗算に依存。 |
| [中国剰余定理 / Chinese Remainder Theorem](crt.md) | 4/5 | 複数の合同式を併合し、最小非負解と周期を求める。 |
| [包除原理・倍数の数え上げ / Inclusion–Exclusion Principle](inclusion.md) | 4/5 | 重複する条件の和集合の大きさを O(2^K) 回の共通部分計算で求める。 |
| [行列積・行列累乗 / Matrix Multiplication and Exponentiation](matrix.md) | 4/5 | 線形な状態遷移の K 回先を O(D³ log K) で求める。 |
| [床関数の和 / Floor Sum](floor-sum.md) | 3/5 | Σ floor((ai+b)/m) を m の対数回の反復で求める。 |
| [ガウス消去・線形基底 / Gaussian Elimination and XOR Basis](gaussian.md) | 3/5 | GF(2) の線形独立性や XOR で表せる値を O(NB) 回の整数演算で求める。 |
| [ミラー–ラビン素数判定 / Miller–Rabin Primality Test](miller-rabin.md) | 3/5 | 64 ビット非負整数の素数判定を少数回の冪剰余で行う。 |
| [約数・倍数ゼータ変換とメビウス反転 / Divisor and Multiple Zeta / Möbius Transforms](multiples-transform.md) | 3/5 | 1〜N の約数和・倍数和を O(N log log N) で求め、逆変換も同じ時間。 |
| [数論変換・高速畳み込み / Number-Theoretic Transform / NTT](ntt.md) | 3/5 | 998244353 を法とする畳み込みを O(L log L) で求める。 |
| [ポラードのρ法・64 ビット素因数分解 / Pollard's Rho Factorization](pollard-rho.md) | 3/5 | 64 ビット整数を素因数分解する。素因数 p の発見は O(√p) 回の反復が目安。 |
