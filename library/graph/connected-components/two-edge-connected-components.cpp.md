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


# :warning: graph/connected-components/two-edge-connected-components.cpp
* category: graph/connected-components


[Back to top page](../../../index.html)



## Code
{% raw %}
```cpp
template< typename G >
struct TwoEdgeConnectedComponents : LowLink< G > {
  using LL = LowLink< G >;
  vector< int > comp;
 
  TwoEdgeConnectedComponents(const G &g) : LL(g) {}
 
  int operator[](const int &k) {
    return comp[k];
  }
 
  void dfs(int idx, int par, int &k) {
    if(~par && this->ord[par] >= this->low[idx]) comp[idx] = comp[par];
    else comp[idx] = k++;
    for(auto &to : this->g[idx]) {
      if(comp[to] == -1) dfs(to, idx, k);
    }
  }
 
  void build(UnWeightedGraph &t) {
    LL::build();
    comp.assign(this->g.size(), -1);
    int k = 0;
    for(int i = 0; i < comp.size(); i++) {
      if(comp[i] == -1) dfs(i, -1, k);
    }
    t.resize(k);
    for(auto &e : this->bridge) {
      int x = comp[e.first], y = comp[e.second];
      t[x].push_back(y);
      t[y].push_back(x);
    }
  }
};

```
{% endraw %}

[Back to top page](../../../index.html)

