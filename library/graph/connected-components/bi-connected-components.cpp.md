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


# :warning: graph/connected-components/bi-connected-components.cpp
<a href="../../../index.html">Back to top page</a>

* category: graph/connected-components
* <a href="{{ site.github.repository_url }}/blob/master/graph/connected-components/bi-connected-components.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 23:02:43 +0900




## Code
{% raw %}
```cpp
template< typename G >
struct BiConnectedComponents : LowLink< G > {
  using LL = LowLink< G >;
 
  vector< int > used;
  vector< vector< pair< int, int > > > bc;
  vector< pair< int, int > > tmp;
 
  BiConnectedComponents(const G &g) : LL(g) {}
 
  void dfs(int idx, int par) {
    used[idx] = true;
    for(auto &to : this->g[idx]) {
      if(to == par) continue;
      if(!used[to] || this->ord[to] < this->ord[idx]) {
        tmp.emplace_back(minmax(idx, to));
      }
      if(!used[to]) {
        dfs(to, idx);
        if(this->low[to] >= this->ord[idx]) {
          bc.emplace_back();
          for(;;) {
            auto e = tmp.back();
            bc.back().emplace_back(e);
            tmp.pop_back();
            if(e.first == min(idx, to) && e.second == max(idx, to)) {
              break;
            }
          }
        }
      }
    }
  }
 
  void build() override {
    LL::build();
    used.assign(this->g.size(), 0);
    for(int i = 0; i < used.size(); i++) {
      if(!used[i]) dfs(i, -1);
    }
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

