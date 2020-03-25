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


# :heavy_check_mark: Offline-Dag-Reachability(DAGの到達可能性クエリ) <small>(graph/others/offline-dag-reachability.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#e557c7f962c39680942b9dada22cabec">graph/others</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/others/offline-dag-reachability.cpp">View this file on GitHub</a>
    - Last commit date: 2020-03-26 01:02:16+09:00




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-0275.test.cpp.html">test/verify/aoj-0275.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Offline-Dag-Reachability(DAGの到達可能性クエリ)
 */
template< typename T >
vector< int > offline_dag_reachability(const Graph< T > &g, vector< pair< int, int > > &qs) {
  const int N = (int) g.size();
  const int Q = (int) qs.size();
  auto ord = topological_sort(g);
  vector< int > ans(Q);
  for(int l = 0; l < Q; l += 64) {
    int r = min(Q, l + 64);
    vector< int64_t > dp(N);
    for(int k = l; k < r; k++) {
      dp[qs[k].first] |= int64_t(1) << (k - l);
    }
    for(auto &idx : ord) {
      for(auto &to : g.g[idx]) dp[to] |= dp[idx];
    }
    for(int k = l; k < r; k++) {
      ans[k] = (dp[qs[k].second] >> (k - l)) & 1;
    }
  }
  return ans;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "graph/others/offline-dag-reachability.cpp"
/**
 * @brief Offline-Dag-Reachability(DAGの到達可能性クエリ)
 */
template< typename T >
vector< int > offline_dag_reachability(const Graph< T > &g, vector< pair< int, int > > &qs) {
  const int N = (int) g.size();
  const int Q = (int) qs.size();
  auto ord = topological_sort(g);
  vector< int > ans(Q);
  for(int l = 0; l < Q; l += 64) {
    int r = min(Q, l + 64);
    vector< int64_t > dp(N);
    for(int k = l; k < r; k++) {
      dp[qs[k].first] |= int64_t(1) << (k - l);
    }
    for(auto &idx : ord) {
      for(auto &to : g.g[idx]) dp[to] |= dp[idx];
    }
    for(int k = l; k < r; k++) {
      ans[k] = (dp[qs[k].second] >> (k - l)) & 1;
    }
  }
  return ans;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

