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


# :heavy_check_mark: Montmort-Number(モンモール数) <small>(math/combinatorics/montmort.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#d319ed68764efb4f50b1628220df55d7">math/combinatorics</a>
* <a href="{{ site.github.repository_url }}/blob/master/math/combinatorics/montmort.cpp">View this file on GitHub</a>
    - Last commit date: 2020-02-24 19:08:02+09:00




## 概要

完全順列の総数をモンモール数とよぶ.

長さ $n$ の完全順列とは, 長さ $n$ の順列であって $i(1 \leq i \leq N)$ 番目の要素が $i$ でない順列を指す.

* `montmort(n)`: `n` 番目のモンモール数を返す.

## 計算量

* $O(n)$


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-montmort-number-mod.test.cpp.html">test/verify/yosupo-montmort-number-mod.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Montmort-Number(モンモール数)
 * @docs docs/montmort.md
 */
template< typename T >
vector< T > montmort(int N) {
  vector< T > dp(N + 1);
  for(int k = 2; k <= N; k++) {
    dp[k] = dp[k - 1] * k;
    if(k & 1) dp[k] -= 1;
    else dp[k] += 1;
  }
  return dp;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "math/combinatorics/montmort.cpp"
/**
 * @brief Montmort-Number(モンモール数)
 * @docs docs/montmort.md
 */
template< typename T >
vector< T > montmort(int N) {
  vector< T > dp(N + 1);
  for(int k = 2; k <= N; k++) {
    dp[k] = dp[k - 1] * k;
    if(k & 1) dp[k] -= 1;
    else dp[k] += 1;
  }
  return dp;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

