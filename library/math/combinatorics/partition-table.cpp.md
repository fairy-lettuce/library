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


# :heavy_check_mark: Partition-Table(分割数テーブル) <small>(math/combinatorics/partition-table.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#d319ed68764efb4f50b1628220df55d7">math/combinatorics</a>
* <a href="{{ site.github.repository_url }}/blob/master/math/combinatorics/partition-table.cpp">View this file on GitHub</a>
    - Last commit date: 2020-02-24 19:08:02+09:00




## 概要

分割数 $P(n, k)$ は整数 $n$ をちょうど $k$ 個の非負整数の和で表す方法の数を与える. 順序が異なるものは同一視する.

* `partition_table(n, k)`: 各 $i \leq n, j \leq k$ に対し分割数 $P(n, k)$ を求める.

## 計算量

* $O(nk)$


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-dpl-5-j.test.cpp.html">test/verify/aoj-dpl-5-j.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Partition-Table(分割数テーブル)
 * @docs docs/partition-table.md
 */
template< typename T >
vector< vector< T > > partition_table(int n, int k) {
  vector< vector< T > > dp(n + 1, vector< T >(k + 1));
  dp[0][0] = 1;
  for(int i = 0; i <= n; i++) {
    for(int j = 1; j <= k; j++) {
      if(i - j >= 0) dp[i][j] = dp[i][j - 1] + dp[i - j][j];
      else dp[i][j] = dp[i][j - 1];
    }
  }
  return dp;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "math/combinatorics/partition-table.cpp"
/**
 * @brief Partition-Table(分割数テーブル)
 * @docs docs/partition-table.md
 */
template< typename T >
vector< vector< T > > partition_table(int n, int k) {
  vector< vector< T > > dp(n + 1, vector< T >(k + 1));
  dp[0][0] = 1;
  for(int i = 0; i <= n; i++) {
    for(int j = 1; j <= k; j++) {
      if(i - j >= 0) dp[i][j] = dp[i][j - 1] + dp[i - j][j];
      else dp[i][j] = dp[i][j - 1];
    }
  }
  return dp;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

