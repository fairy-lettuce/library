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


# :heavy_check_mark: Tree-Diameter(木の直径) <small>(graph/tree/tree-diameter.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#28790b6202284cbbffc9d712b59f4b80">graph/tree</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/tree/tree-diameter.cpp">View this file on GitHub</a>
    - Last commit date: 2020-09-15 01:41:10+09:00




## Depends on

* :heavy_check_mark: <a href="../graph-template.cpp.html">graph/graph-template.cpp</a>


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-grl-5-a.test.cpp.html">test/verify/aoj-grl-5-a.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-tree-diameter.test.cpp.html">test/verify/yosupo-tree-diameter.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#include "../graph-template.cpp"

/**
 * @brief Tree-Diameter(木の直径)
 */
template< typename T = int >
struct TreeDiameter : Graph< T > {
public:
  using Graph< T >::Graph;
  using Graph< T >::g;
  vector< Edge< T > > path;

  T build() {
    to.assign(g.size(), -1);
    auto p = dfs(0, -1);
    auto q = dfs(p.second, -1);

    int now = p.second;
    while(now != q.second) {
      for(auto &e : g[now]) {
        if(to[now] == e.to) {
          path.emplace_back(e);
        }
      }
      now = to[now];
    }
    return q.first;
  }

  explicit TreeDiameter(const Graph< T > &g) : Graph< T >(g) {}

private:
  vector< int > to;

  pair< T, int > dfs(int idx, int par) {
    pair< T, int > ret(0, idx);
    for(auto &e : g[idx]) {
      if(e.to == par) continue;
      auto cost = dfs(e.to, idx);
      cost.first += e.cost;
      if(ret < cost) {
        ret = cost;
        to[idx] = e.to;
      }
    }
    return ret;
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 2 "graph/graph-template.cpp"

template< typename T = int >
struct Edge {
  int from, to;
  T cost;
  int idx;

  Edge() = default;

  Edge(int from, int to, T cost = 1, int idx = -1) : from(from), to(to), cost(cost), idx(idx) {}

  operator int() const { return to; }
};

template< typename T = int >
struct Graph {
  vector< vector< Edge< T > > > g;
  int es;

  Graph() = default;

  explicit Graph(int n) : g(n), es(0) {}

  size_t size() const {
    return g.size();
  }

  void add_directed_edge(int from, int to, T cost = 1) {
    g[from].emplace_back(from, to, cost, es++);
  }

  void add_edge(int from, int to, T cost = 1) {
    g[from].emplace_back(from, to, cost, es);
    g[to].emplace_back(to, from, cost, es++);
  }

  void read(int M, int padding = -1, bool weighted = false, bool directed = false) {
    for(int i = 0; i < M; i++) {
      int a, b;
      cin >> a >> b;
      a += padding;
      b += padding;
      T c = T(1);
      if(weighted) cin >> c;
      if(directed) add_directed_edge(a, b, c);
      else add_edge(a, b, c);
    }
  }
};

template< typename T = int >
using Edges = vector< Edge< T > >;
#line 2 "graph/tree/tree-diameter.cpp"

/**
 * @brief Tree-Diameter(木の直径)
 */
template< typename T = int >
struct TreeDiameter : Graph< T > {
public:
  using Graph< T >::Graph;
  using Graph< T >::g;
  vector< Edge< T > > path;

  T build() {
    to.assign(g.size(), -1);
    auto p = dfs(0, -1);
    auto q = dfs(p.second, -1);

    int now = p.second;
    while(now != q.second) {
      for(auto &e : g[now]) {
        if(to[now] == e.to) {
          path.emplace_back(e);
        }
      }
      now = to[now];
    }
    return q.first;
  }

  explicit TreeDiameter(const Graph< T > &g) : Graph< T >(g) {}

private:
  vector< int > to;

  pair< T, int > dfs(int idx, int par) {
    pair< T, int > ret(0, idx);
    for(auto &e : g[idx]) {
      if(e.to == par) continue;
      auto cost = dfs(e.to, idx);
      cost.first += e.cost;
      if(ret < cost) {
        ret = cost;
        to[idx] = e.to;
      }
    }
    return ret;
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

