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


# :warning: Binomial-Table(二項係数テーブル) <small>(math/combinatorics/binomial-table.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#d319ed68764efb4f50b1628220df55d7">math/combinatorics</a>
* <a href="{{ site.github.repository_url }}/blob/master/math/combinatorics/binomial-table.cpp">View this file on GitHub</a>
    - Last commit date: 2020-02-24 19:08:02+09:00




## 概要

二項係数テーブルをパスカルの三角形より求める.

* `binomial_table(n)`: `n` 以下の二項係数テーブルを返す.

## 計算量

* $O(n^2)$


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Binomial-Table(二項係数テーブル)
 * @docs docs/binomial-table.md
 */
template< typename T >
vector< vector< T > > binomial_table(int N) {
  vector< vector< T > > mat(N + 1, vector< T >(N + 1));
  for(int i = 0; i <= N; i++) {
    for(int j = 0; j <= i; j++) {
      if(j == 0 || j == i) mat[i][j] = 1;
      else mat[i][j] = mat[i - 1][j - 1] + mat[i - 1][j];
    }
  }
  return mat;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "math/combinatorics/binomial-table.cpp"
/**
 * @brief Binomial-Table(二項係数テーブル)
 * @docs docs/binomial-table.md
 */
template< typename T >
vector< vector< T > > binomial_table(int N) {
  vector< vector< T > > mat(N + 1, vector< T >(N + 1));
  for(int i = 0; i <= N; i++) {
    for(int j = 0; j <= i; j++) {
      if(j == 0 || j == i) mat[i][j] = 1;
      else mat[i][j] = mat[i - 1][j - 1] + mat[i - 1][j];
    }
  }
  return mat;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

