---
layout: default
---

<!-- mathjax config similar to math.stackexchange -->
<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    TeX: { equationNumbers: { autoNumber: "AMS" }},
    tex2jax: {
      inlineMath: [ ['$','$'] ],
      processEscapes: true
    },
    "HTML-CSS": { matchFontHeight: false },
    displayAlign: "left",
    displayIndent: "2em"
  });
</script>

<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/jquery-balloon-js@1.1.2/jquery.balloon.min.js" integrity="sha256-ZEYs9VrgAeNuPvs15E39OsyOJaIkXEEt10fzxJ20+2I=" crossorigin="anonymous"></script>
<script type="text/javascript" src="../../../assets/js/copy-button.js"></script>
<link rel="stylesheet" href="../../../assets/css/copy-button.css" />


# :heavy_check_mark: Disjoint-Sparse-Table <small>(structure/others/disjoint-sparse-table.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#40d73e22b7d986e3399449c25c8b23a1">structure/others</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/others/disjoint-sparse-table.cpp">View this file on GitHub</a>
    - Last commit date: 2020-02-20 22:23:04+09:00


## 概要

更新がない場合の半群に対する区間クエリを, 前計算 $O(n \log n)$, クエリ $O(1)$ で処理する.

* $\mathrm{DisjointSparseTable}(v, f)$: 配列 $v$ で初期化する. $f$ は半群をマージする二項演算である.
* $\mathrm{query}(l, r)$: 区間 $[l, r)$ の最小値を求める.


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-staticrmq-2.test.cpp.html">test/verify/yosupo-staticrmq-2.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Disjoint-Sparse-Table
 * @docs docs/disjoint-sparse-table.md
 */
template< typename Semigroup >
struct DisjointSparseTable {
  using F = function< Semigroup(Semigroup, Semigroup) >;
  const F f;
  vector< vector< Semigroup > > st;
  vector< int > lookup;

  DisjointSparseTable(const vector< Semigroup > &v, const F &f) : f(f) {
    int b = 0;
    while((1 << b) <= v.size()) ++b;
    st.resize(b, vector< Semigroup >(v.size(), Semigroup()));
    for(int i = 0; i < v.size(); i++) st[0][i] = v[i];
    for(int i = 1; i < b; i++) {
      int shift = 1 << i;
      for(int j = 0; j < v.size(); j += shift << 1) {
        int t = min(j + shift, (int) v.size());
        st[i][t - 1] = v[t - 1];
        for(int k = t - 2; k >= j; k--) st[i][k] = f(v[k], st[i][k + 1]);
        if(v.size() <= t) break;
        st[i][t] = v[t];
        int r = min(t + shift, (int) v.size());
        for(int k = t + 1; k < r; k++) st[i][k] = f(st[i][k - 1], v[k]);
      }
    }
    lookup.resize(1 << b);
    for(int i = 2; i < lookup.size(); i++) {
      lookup[i] = lookup[i >> 1] + 1;
    }
  }

  Semigroup query(int l, int r) {
    if(l >= --r) return st[0][l];
    int p = lookup[l ^ r];
    return f(st[p][l], st[p][r]);
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/others/disjoint-sparse-table.cpp"
/**
 * @brief Disjoint-Sparse-Table
 * @docs docs/disjoint-sparse-table.md
 */
template< typename Semigroup >
struct DisjointSparseTable {
  using F = function< Semigroup(Semigroup, Semigroup) >;
  const F f;
  vector< vector< Semigroup > > st;
  vector< int > lookup;

  DisjointSparseTable(const vector< Semigroup > &v, const F &f) : f(f) {
    int b = 0;
    while((1 << b) <= v.size()) ++b;
    st.resize(b, vector< Semigroup >(v.size(), Semigroup()));
    for(int i = 0; i < v.size(); i++) st[0][i] = v[i];
    for(int i = 1; i < b; i++) {
      int shift = 1 << i;
      for(int j = 0; j < v.size(); j += shift << 1) {
        int t = min(j + shift, (int) v.size());
        st[i][t - 1] = v[t - 1];
        for(int k = t - 2; k >= j; k--) st[i][k] = f(v[k], st[i][k + 1]);
        if(v.size() <= t) break;
        st[i][t] = v[t];
        int r = min(t + shift, (int) v.size());
        for(int k = t + 1; k < r; k++) st[i][k] = f(st[i][k - 1], v[k]);
      }
    }
    lookup.resize(1 << b);
    for(int i = 2; i < lookup.size(); i++) {
      lookup[i] = lookup[i >> 1] + 1;
    }
  }

  Semigroup query(int l, int r) {
    if(l >= --r) return st[0][l];
    int p = lookup[l ^ r];
    return f(st[p][l], st[p][r]);
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

