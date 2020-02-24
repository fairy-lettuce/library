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


# :heavy_check_mark: Sparse-Table(スパーステーブル) <small>(structure/others/sparse-table.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#40d73e22b7d986e3399449c25c8b23a1">structure/others</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/others/sparse-table.cpp">View this file on GitHub</a>
    - Last commit date: 2020-02-20 22:23:04+09:00




## 概要

更新がない場合の区間の最小値を, 前計算 $O(n \log n)$, クエリ $O(1)$ で処理する.

* `SparseTable(v)`: 配列 `v` で初期化する.
* `query(l, r)`: 区間 $[l, r)$ の最小値を求める.

## 計算量

* `SparseTable(v)`: $O(N \log N)$
* `query(l, r)`: $O(1)$


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-staticrmq.test.cpp.html">test/verify/yosupo-staticrmq.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Sparse-Table(スパーステーブル)
 * @docs docs/sparse-table.md
 */
template< typename T >
struct SparseTable {
  vector< vector< T > > st;
  vector< int > lookup;

  explicit SparseTable(const vector< T > &v) {
    int b = 0;
    while((1 << b) <= v.size()) ++b;
    st.assign(b, vector< T >(1 << b));
    for(int i = 0; i < v.size(); i++) {
      st[0][i] = v[i];
    }
    for(int i = 1; i < b; i++) {
      for(int j = 0; j + (1 << i) <= (1 << b); j++) {
        st[i][j] = min(st[i - 1][j], st[i - 1][j + (1 << (i - 1))]);
      }
    }
    lookup.resize(v.size() + 1);
    for(int i = 2; i < lookup.size(); i++) {
      lookup[i] = lookup[i >> 1] + 1;
    }
  }

  inline T query(int l, int r) const {
    int b = lookup[r - l];
    return min(st[b][l], st[b][r - (1 << b)]);
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/others/sparse-table.cpp"
/**
 * @brief Sparse-Table(スパーステーブル)
 * @docs docs/sparse-table.md
 */
template< typename T >
struct SparseTable {
  vector< vector< T > > st;
  vector< int > lookup;

  explicit SparseTable(const vector< T > &v) {
    int b = 0;
    while((1 << b) <= v.size()) ++b;
    st.assign(b, vector< T >(1 << b));
    for(int i = 0; i < v.size(); i++) {
      st[0][i] = v[i];
    }
    for(int i = 1; i < b; i++) {
      for(int j = 0; j + (1 << i) <= (1 << b); j++) {
        st[i][j] = min(st[i - 1][j], st[i - 1][j + (1 << (i - 1))]);
      }
    }
    lookup.resize(v.size() + 1);
    for(int i = 2; i < lookup.size(); i++) {
      lookup[i] = lookup[i >> 1] + 1;
    }
  }

  inline T query(int l, int r) const {
    int b = lookup[r - l];
    return min(st[b][l], st[b][r - (1 << b)]);
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

