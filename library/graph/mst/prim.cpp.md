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


# :warning: graph/mst/prim.cpp
<a href="../../../index.html">Back to top page</a>

* category: graph/mst
* <a href="{{ site.github.repository_url }}/blob/master/graph/mst/prim.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 23:02:43 +0900




## Verified With
* :warning: <a href="../../../verify/test/verify/aoj-grl-2-a.test.cpp.html">test/verify/aoj-grl-2-a.test.cpp</a>


## Code
{% raw %}
```cpp
template< typename T >
T prim(WeightedGraph< T > &g) {
  using Pi = pair< T, int >;
 
  T total = 0;
  vector< bool > used(g.size(), false);
  priority_queue< Pi, vector< Pi >, greater< Pi > > que;
  que.emplace(0, 0);
  while(!que.empty()) {
    auto p = que.top();
    que.pop();
    if(used[p.second]) continue;
    used[p.second] = true;
    total += p.first;
    for(auto &e : g[p.second]) {
      que.emplace(e.cost, e.to);
    }
  }
  return total;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

