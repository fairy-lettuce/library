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


# :question: Centroid-Decomosition(重心分解) <small>(graph/tree/centroid-decomposition.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#28790b6202284cbbffc9d712b59f4b80">graph/tree</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/tree/centroid-decomposition.cpp">View this file on GitHub</a>
    - Last commit date: 2020-09-15 01:04:53+09:00




## Depends on

* :question: <a href="../graph-template.cpp.html">graph/graph-template.cpp</a>


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-3139.test.cpp.html">test/verify/aoj-3139.test.cpp</a>
* :x: <a href="../../../verify/test/verify/yosupo-frequency-table-of-tree-distance.test.cpp.html">test/verify/yosupo-frequency-table-of-tree-distance.test.cpp</a>
* :x: <a href="../../../verify/test/verify/yukicoder-1002.test.cpp.html">test/verify/yukicoder-1002.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#include "../graph-template.cpp"

/**
 * @brief Centroid-Decomosition(重心分解)
 */
template< typename T >
struct CentroidDecomposition : Graph< T > {
public:
  using Graph< T >::Graph;
  using Graph< T >::g;
  Graph< int > tree;

  int build(int t = 0) {
    sub.assign(g.size(), 0);
    v.assign(g.size(), 0);
    tree = Graph< T >(g.size());
    return build_dfs(0);
  }

  explicit CentroidDecomposition(const Graph< T > &g) : Graph< T >(g) {}

private:
  vector< int > sub;
  vector< int > v;

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

  inline int build_dfs(int idx) {
    int centroid = search_centroid(idx, -1, build_dfs(idx, -1) / 2);
    v[centroid] = true;
    for(auto &to : g[centroid]) {
      if(!v[to]) tree.add_directed_edge(centroid, build_dfs(to));
    }
    v[centroid] = false;
    return centroid;
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
#line 2 "graph/tree/centroid-decomposition.cpp"

/**
 * @brief Centroid-Decomosition(重心分解)
 */
template< typename T >
struct CentroidDecomposition : Graph< T > {
public:
  using Graph< T >::Graph;
  using Graph< T >::g;
  Graph< int > tree;

  int build(int t = 0) {
    sub.assign(g.size(), 0);
    v.assign(g.size(), 0);
    tree = Graph< T >(g.size());
    return build_dfs(0);
  }

  explicit CentroidDecomposition(const Graph< T > &g) : Graph< T >(g) {}

private:
  vector< int > sub;
  vector< int > v;

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

  inline int build_dfs(int idx) {
    int centroid = search_centroid(idx, -1, build_dfs(idx, -1) / 2);
    v[centroid] = true;
    for(auto &to : g[centroid]) {
      if(!v[to]) tree.add_directed_edge(centroid, build_dfs(to));
    }
    v[centroid] = false;
    return centroid;
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

