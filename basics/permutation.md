# 置換・順列の巡回分解 / Permutation and Cycle Decomposition

**4/5** · 置換を O(N) で周期に分解し、K 回先をまとめて求める。

## 使い方

permutation_power(p,k)[v] は p を k 回適用した位置。p は 0〜N-1 の置換。k<0 なら逆向き。

## コード

```python
def permutation_power(p, k):
    ans = [-1] * len(p)
    for s in range(len(p)):
        if ans[s] >= 0:
            continue
        cycle = [s]
        v = p[s]
        while v != s:
            cycle.append(v)
            v = p[v]
        step = k % len(cycle)
        for i, v in enumerate(cycle):
            ans[v] = cycle[(i+step) % len(cycle)]
    return ans
```

## 考え方

置換では全頂点が閉路に属し、閉路に流れ込む外側の頂点は存在しない。各閉路内で移動回数を長さで割った余りにできる。置換全体の周期は各閉路長の最小公倍数。

### 例題

```python
assert permutation_power([1,2,0,3], 5) == [2,0,1,3]
```

[分野の目次](README.md) · [全体の目次](../README.md)
