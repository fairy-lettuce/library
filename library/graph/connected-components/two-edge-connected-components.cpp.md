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


# :heavy_check_mark: Two-Edge-Connected-Components(二重辺連結成分分解) <small>(graph/connected-components/two-edge-connected-components.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#3a7c46e10de1b2cce1293b2074b86f0a">graph/connected-components</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/connected-components/two-edge-connected-components.cpp">View this file on GitHub</a>
    - Last commit date: 2020-03-25 22:02:49+09:00




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-two-edge-connected-components.test.cpp.html">test/verify/yosupo-two-edge-connected-components.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Two-Edge-Connected-Components(二重辺連結成分分解)
 */
template< typename T = int >
struct TwoEdgeConnectedComponents : LowLink< T > {
public:
  using LowLink< T >::LowLink;
  using LowLink< T >::g;
  using LowLink< T >::ord;
  using LowLink< T >::low;
  using LowLink< T >::bridge;

  vector< int > comp;
  Graph< T > tree;
  vector< vector< int > > group;

  int operator[](const int &k) const {
    return comp[k];
  }

  void build() override {
    LowLink< T >::build();
    comp.assign(g.size(), -1);
    int k = 0;
    for(int i = 0; i < (int) comp.size(); i++) {
      if(comp[i] == -1) dfs(i, -1, k);
    }
    group.resize(k);
    for(int i = 0; i < (int) g.size(); i++) {
      group[comp[i]].emplace_back(i);
    }
    tree = Graph< T >(k);
    for(auto &e : bridge) {
      tree.add_edge(comp[e.from], comp[e.to], e.cost);
    }
  }

  explicit TwoEdgeConnectedComponents(const Graph< T > &g) : Graph< T >(g) {}

private:
  void dfs(int idx, int par, int &k) {
    if(par >= 0 && ord[par] >= low[idx]) comp[idx] = comp[par];
    else comp[idx] = k++;
    for(auto &to : g[idx]) {
      if(comp[to] == -1) dfs(to, idx, k);
    }
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "graph/connected-components/two-edge-connected-components.cpp"
/**
 * @brief Two-Edge-Connected-Components(二重辺連結成分分解)
 */
template< typename T = int >
struct TwoEdgeConnectedComponents : LowLink< T > {
public:
  using LowLink< T >::LowLink;
  using LowLink< T >::g;
  using LowLink< T >::ord;
  using LowLink< T >::low;
  using LowLink< T >::bridge;

  vector< int > comp;
  Graph< T > tree;
  vector< vector< int > > group;

  int operator[](const int &k) const {
    return comp[k];
  }

  void build() override {
    LowLink< T >::build();
    comp.assign(g.size(), -1);
    int k = 0;
    for(int i = 0; i < (int) comp.size(); i++) {
      if(comp[i] == -1) dfs(i, -1, k);
    }
    group.resize(k);
    for(int i = 0; i < (int) g.size(); i++) {
      group[comp[i]].emplace_back(i);
    }
    tree = Graph< T >(k);
    for(auto &e : bridge) {
      tree.add_edge(comp[e.from], comp[e.to], e.cost);
    }
  }

  explicit TwoEdgeConnectedComponents(const Graph< T > &g) : Graph< T >(g) {}

private:
  void dfs(int idx, int par, int &k) {
    if(par >= 0 && ord[par] >= low[idx]) comp[idx] = comp[par];
    else comp[idx] = k++;
    for(auto &to : g[idx]) {
      if(comp[to] == -1) dfs(to, idx, k);
    }
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

