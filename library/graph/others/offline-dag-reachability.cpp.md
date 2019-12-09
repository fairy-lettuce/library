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


# :warning: graph/others/offline-dag-reachability.cpp
* category: graph/others


[Back to top page](../../../index.html)



## Verified
* :heavy_check_mark: [test/verify/aoj-0275.test.cpp](../../../verify/test/verify/aoj-0275.test.cpp.html)


## Code
{% raw %}
```cpp
template< typename G >
vector< int > offline_dag_reachability(const G &g, vector< pair< int, int > > &qs) {
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
      for(auto &to : g[idx]) dp[to] |= dp[idx];
    }
    for(int k = l; k < r; k++) {
      ans[k] = (dp[qs[k].second] >> (k - l)) & 1;
    }
  }
  return ans;
}

```
{% endraw %}

[Back to top page](../../../index.html)

