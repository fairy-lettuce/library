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


# :warning: graph/tree/tree-diameter.cpp
<a href="../../../index.html">Back to top page</a>

* category: graph/tree
* <a href="{{ site.github.repository_url }}/blob/master/graph/tree/tree-diameter.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 23:02:43 +0900




## Verified With
* :warning: <a href="../../../verify/test/verify/aoj-grl-5-a.test.cpp.html">test/verify/aoj-grl-5-a.test.cpp</a>


## Code
{% raw %}
```cpp
template< typename T >
pair< T, int > dfs(const WeightedGraph< T > &g, int idx, int par) {
  pair< T, int > ret(0, idx);
  for(auto &e : g[idx]) {
    if(e.to == par) continue;
    auto cost = dfs(g, e.to, idx);
    cost.first += e.cost;
    ret = max(ret, cost);
  }
  return ret;
}

template< typename T >
T tree_diameter(const WeightedGraph< T > &g) {
  auto p = dfs(g, 0, -1);
  auto q = dfs(g, p.second, -1);
  return (q.first);
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

