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


# :warning: graph/tree/centroid-decomposition.cpp
<a href="../../../index.html">Back to top page</a>

* category: graph/tree
* <a href="{{ site.github.repository_url }}/blob/master/graph/tree/centroid-decomposition.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 23:02:43 +0900




## Code
{% raw %}
```cpp
template< typename G >
struct CentroidDecomposition {
  const G &g;
  vector< int > sub;
  vector< vector< int > > belong;
  vector< bool > v;

  CentroidDecomposition(const G &g) : g(g), sub(g.size()), v(g.size()), belong(g.size()) {}

  inline int build_dfs(int idx, int par) {
    sub[idx] = 1;
    for(auto &to : g[idx]) {
      if(to == par || v[to]) continue;
      sub[idx] += build_dfs(to, idx);
    }
    return sub[idx];
  }

  inline int search_centroid(int idx, int par, const int mid) {
    for(auto &to : g[idx]) {
      if(to == par || v[to]) continue;
      if(sub[to] > mid) return search_centroid(to, idx, mid);
    }
    return idx;
  }

  inline void belong_dfs(int idx, int par, int centroid) {
    belong[idx].emplace_back(centroid);
    for(auto &to : g[idx]) {
      if(to == par || v[to]) continue;
      belong_dfs(to, idx, centroid);
    }
  }

  inline int build(UnWeightedGraph &t, int idx) {
    int centroid = search_centroid(idx, -1, build_dfs(idx, -1) / 2);
    v[centroid] = true;
    belong_dfs(centroid, -1, centroid);
    for(auto &to : g[centroid]) {
      if(!v[to]) t[centroid].emplace_back(build(t, to));
    }
    v[centroid] = false;
    return centroid;
  }

  inline int build(UnWeightedGraph &t) {
    t.resize(g.size());
    return build(t, 0);
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

