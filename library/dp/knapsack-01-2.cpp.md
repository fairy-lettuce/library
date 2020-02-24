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


# :heavy_check_mark: Knapsack-01(0-1ナップサック問題) $O(N \sum {v_i})$ <small>(dp/knapsack-01-2.cpp)</small>

<a href="../../index.html">Back to top page</a>

* category: <a href="../../index.html#95687afb5d9a2a9fa39038f991640b0c">dp</a>
* <a href="{{ site.github.repository_url }}/blob/master/dp/knapsack-01-2.cpp">View this file on GitHub</a>
    - Last commit date: 2020-02-21 17:07:30+09:00




## 概要

0-1 ナップサック問題を次に示す.

重さ $w_i$, 価値 $v_i$ であるような $N$ 個の品物がある. 重さの和が $W$ 以下となるように選ぶとき, 価値の最大値を求めよ.

価値を状態にした動的計画法により $O(N \sum {v_i})$. 

* `knapsack_01_2(w, v, W)`: 重さが `W` 以下で価値の和の最大値を返す.


## Verified with

* :heavy_check_mark: <a href="../../verify/test/verify/aoj-dpl-1-f.test.cpp.html">test/verify/aoj-dpl-1-f.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Knapsack-01(0-1ナップサック問題) $O(N \sum {v_i})$
 * @docs docs/knapsack-01-2.md
 */
template< typename T >
T knapsack_01_2(const vector< T > &w, const vector< int > &v, const T &W) {
  const int N = (int) w.size();
  const int sum = accumulate(begin(v), end(v), 0);
  vector< T > dp(sum + 1, W + 1);
  dp[0] = T();
  for(int i = 0; i < N; i++) {
    for(int j = sum; j >= v[i]; j--) {
      dp[j] = min(dp[j], dp[j - v[i]] + w[i]);
    }
  }
  int ret = 0;
  for(int i = 0; i <= sum; i++) {
    if(dp[i] <= W) ret = i;
  }
  return ret;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "dp/knapsack-01-2.cpp"
/**
 * @brief Knapsack-01(0-1ナップサック問題) $O(N \sum {v_i})$
 * @docs docs/knapsack-01-2.md
 */
template< typename T >
T knapsack_01_2(const vector< T > &w, const vector< int > &v, const T &W) {
  const int N = (int) w.size();
  const int sum = accumulate(begin(v), end(v), 0);
  vector< T > dp(sum + 1, W + 1);
  dp[0] = T();
  for(int i = 0; i < N; i++) {
    for(int j = sum; j >= v[i]; j--) {
      dp[j] = min(dp[j], dp[j - v[i]] + w[i]);
    }
  }
  int ret = 0;
  for(int i = 0; i <= sum; i++) {
    if(dp[i] <= W) ret = i;
  }
  return ret;
}

```
{% endraw %}

<a href="../../index.html">Back to top page</a>

