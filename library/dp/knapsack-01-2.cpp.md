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


# :heavy_check_mark: dp/knapsack-01-2.cpp

<a href="../../index.html">Back to top page</a>

* category: <a href="../../index.html#95687afb5d9a2a9fa39038f991640b0c">dp</a>
* <a href="{{ site.github.repository_url }}/blob/master/dp/knapsack-01-2.cpp">View this file on GitHub</a>
    - Last commit date: 2019-12-23 02:27:30+09:00




## Verified with

* :heavy_check_mark: <a href="../../verify/test/verify/aoj-dpl-1-f.test.cpp.html">test/verify/aoj-dpl-1-f.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
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

