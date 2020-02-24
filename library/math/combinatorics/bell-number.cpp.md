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


# :heavy_check_mark: Bell-Number(ベル数) <small>(math/combinatorics/bell-number.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#d319ed68764efb4f50b1628220df55d7">math/combinatorics</a>
* <a href="{{ site.github.repository_url }}/blob/master/math/combinatorics/bell-number.cpp">View this file on GitHub</a>
    - Last commit date: 2020-02-24 19:08:02+09:00




## 概要

ベル数 $B(n,k)$ を求める.

区別できる $n$ 個のボールを区別できない $k$ 個以下の箱に分割する方法の数を与える.

特に $B(n,n)$ は $n$ 個のボールを任意個のグループに分割する方法の数である.

* `bell_number(n, k)`: $B(n, k)$ を返す.

## 計算量

* $O(\min(n, k) \log n)$


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-dpl-5-g.test.cpp.html">test/verify/aoj-dpl-5-g.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Bell-Number(ベル数)
 * @docs docs/bell-number.md
 */
template< typename T >
T bell_number(int n, int k) {
  if(n == 0) return 1;
  k = min(k, n);
  Combination< T > uku(k);
  T ret = 0;
  vector< T > pref(k + 1);
  pref[0] = 1;
  for(int i = 1; i <= k; i++) {
    if(i & 1) pref[i] = pref[i - 1] - uku.rfact(i);
    else pref[i] = pref[i - 1] + uku.rfact(i);
  }
  for(int i = 1; i <= k; i++) {
    ret += T(i).pow(n) * uku.rfact(i) * pref[k - i];
  }
  return ret;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "math/combinatorics/bell-number.cpp"
/**
 * @brief Bell-Number(ベル数)
 * @docs docs/bell-number.md
 */
template< typename T >
T bell_number(int n, int k) {
  if(n == 0) return 1;
  k = min(k, n);
  Combination< T > uku(k);
  T ret = 0;
  vector< T > pref(k + 1);
  pref[0] = 1;
  for(int i = 1; i <= k; i++) {
    if(i & 1) pref[i] = pref[i - 1] - uku.rfact(i);
    else pref[i] = pref[i - 1] + uku.rfact(i);
  }
  for(int i = 1; i <= k; i++) {
    ret += T(i).pow(n) * uku.rfact(i) * pref[k - i];
  }
  return ret;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

