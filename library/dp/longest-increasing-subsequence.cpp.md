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
<script type="text/javascript" src="../../assets/js/copy-button.js"></script>
<link rel="stylesheet" href="../../assets/css/copy-button.css" />


# :heavy_check_mark: Longest-Increasing-Subsequence(最長増加部分列) <small>(dp/longest-increasing-subsequence.cpp)</small>

<a href="../../index.html">Back to top page</a>

* category: <a href="../../index.html#95687afb5d9a2a9fa39038f991640b0c">dp</a>
* <a href="{{ site.github.repository_url }}/blob/master/dp/longest-increasing-subsequence.cpp">View this file on GitHub</a>
    - Last commit date: 2020-02-26 02:30:05+09:00




## 概要

最長増加部分列(LIS)の長さを求める.

`lis[i]` を、現状態で長さ $i$ 以下の増加部分列を作るときの最後の要素の最小値と定義する. このとき `lis[i]` は常に単調増加になっている.

数列の要素を左からみる. 二分探索で `lis[k]` が現在の要素以下(未満) となる最大の $k$ を求め, `lis[k+1]` を現在の要素に書き換えることを繰り返すことで LIS を求めることができる.

ここでは実装しない(←実装しなさーい！)が別のアルゴリズムとして, `lis[i]` を現状態で最後の要素が値 $i$ の増加部分列を作るときの最長の長さと定義する方法も存在する. 数列の要素を左から見ていって, 現在の値の要素以下(未満) で最大の `lis[k]` $+ 1$ を求めることで更新出来て, これは BIT や セグメント木を使って効率的に求めることができる.

* `longest_increasing_subsequence(a, strict)`: 数列 `a` の最長増加部分列の長さを求める.`strict` が `true` のとき狭義(厳密に増加する列), `false` のとき広義で求める.

## 計算量

* $O(N \log N)$


## Verified with

* :heavy_check_mark: <a href="../../verify/test/verify/aoj-dpl-1-d.test.cpp.html">test/verify/aoj-dpl-1-d.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Longest-Increasing-Subsequence(最長増加部分列)
 * @docs docs/longest-increasing-subsequence.md
 */
template< typename T >
size_t longest_increasing_subsequence(const vector< T > &a, bool strict) {
  vector< T > lis;
  for(auto &p : a) {
    typename vector< T >::iterator it;
    if(strict) it = lower_bound(begin(lis), end(lis), p);
    else it = upper_bound(begin(lis), end(lis), p);
    if(end(lis) == it) lis.emplace_back(p);
    else *it = p;
  }
  return lis.size();
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "dp/longest-increasing-subsequence.cpp"
/**
 * @brief Longest-Increasing-Subsequence(最長増加部分列)
 * @docs docs/longest-increasing-subsequence.md
 */
template< typename T >
size_t longest_increasing_subsequence(const vector< T > &a, bool strict) {
  vector< T > lis;
  for(auto &p : a) {
    typename vector< T >::iterator it;
    if(strict) it = lower_bound(begin(lis), end(lis), p);
    else it = upper_bound(begin(lis), end(lis), p);
    if(end(lis) == it) lis.emplace_back(p);
    else *it = p;
  }
  return lis.size();
}

```
{% endraw %}

<a href="../../index.html">Back to top page</a>

