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


# :heavy_check_mark: Bi-Connected-Components(二重頂点連結成分分解) <small>(graph/connected-components/bi-connected-components.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#3a7c46e10de1b2cce1293b2074b86f0a">graph/connected-components</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/connected-components/bi-connected-components.cpp">View this file on GitHub</a>
    - Last commit date: 2020-09-15 01:04:53+09:00




## 概要

二重連結成分分解とも. 二重頂点連結成分とは, $1$ 個の頂点を取り除いても連結である部分グラフである. 

関節点は, その頂点とそれを端点とする辺を削除したときの部分グラフが非連結になるような頂点を指す. したがって, 関節点を列挙した後に頑張ると列挙できる.


* `build()`: 二重頂点連結成分分解する. `bc` には各二重頂点連結成分に属する辺が格納される.

## 計算量

* $O(E + V)$


## Depends on

* :question: <a href="../graph-template.cpp.html">graph/graph-template.cpp</a>
* :question: <a href="../others/low-link.cpp.html">Low-Link(橋/関節点) <small>(graph/others/low-link.cpp)</small></a>


## Required by

* :heavy_check_mark: <a href="../others/block-cut-tree.cpp.html">Block-Cut-Tree <small>(graph/others/block-cut-tree.cpp)</small></a>


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-3022.test.cpp.html">test/verify/aoj-3022.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-3139.test.cpp.html">test/verify/aoj-3139.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#include "../others/low-link.cpp"

/**
 * @brief Bi-Connected-Components(二重頂点連結成分分解)
 * @docs docs/bi-connected-components.md
 */
template< typename T = int >
struct BiConnectedComponents : LowLink< T > {
public:
  using LowLink< T >::LowLink;
  using LowLink< T >::g;
  using LowLink< T >::ord;
  using LowLink< T >::low;

  vector< vector< Edge< T > > > bc;

  void build() override {
    LowLink< T >::build();
    used.assign(g.size(), 0);
    for(int i = 0; i < used.size(); i++) {
      if(!used[i]) dfs(i, -1);
    }
  }

  explicit BiConnectedComponents(const Graph< T > &g) : Graph< T >(g) {}

private:
  vector< int > used;
  vector< Edge< T > > tmp;

  void dfs(int idx, int par) {
    used[idx] = true;
    bool beet = false;
    for(auto &to : g[idx]) {
      if(to == par && !exchange(beet, true)) continue;
      if(!used[to] || ord[to] < ord[idx]) {
        tmp.emplace_back(to);
      }
      if(!used[to]) {
        dfs(to, idx);
        if(low[to] >= ord[idx]) {
          bc.emplace_back();
          for(;;) {
            auto e = tmp.back();
            bc.back().emplace_back(e);
            tmp.pop_back();
            if(e.idx == to.idx) break;
          }
        }
      }
    }
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
#line 2 "graph/others/low-link.cpp"

/**
 * @brief Low-Link(橋/関節点)
 * @see http://kagamiz.hatenablog.com/entry/2013/10/05/005213
 * @docs docs/low-link.md
 */
template< typename T = int >
struct LowLink : Graph< T > {
public:
  using Graph< T >::Graph;
  vector< int > ord, low, articulation;
  vector< Edge< T > > bridge;
  using Graph< T >::g;

  virtual void build() {
    used.assign(g.size(), 0);
    ord.assign(g.size(), 0);
    low.assign(g.size(), 0);
    int k = 0;
    for(int i = 0; i < (int) g.size(); i++) {
      if(!used[i]) k = dfs(i, k, -1);
    }
  }

  explicit LowLink(const Graph< T > &g) : Graph< T >(g) {}

private:
  vector< int > used;

  int dfs(int idx, int k, int par) {
    used[idx] = true;
    ord[idx] = k++;
    low[idx] = ord[idx];
    bool is_articulation = false, beet = false;
    int cnt = 0;
    for(auto &to : g[idx]) {
      if(to == par && !exchange(beet, true)) {
        continue;
      }
      if(!used[to]) {
        ++cnt;
        k = dfs(to, k, idx);
        low[idx] = min(low[idx], low[to]);
        is_articulation |= par >= 0 && low[to] >= ord[idx];
        if(ord[idx] < low[to]) bridge.emplace_back(to);
      } else {
        low[idx] = min(low[idx], ord[to]);
      }
    }
    is_articulation |= par == -1 && cnt > 1;
    if(is_articulation) articulation.push_back(idx);
    return k;
  }
};
#line 2 "graph/connected-components/bi-connected-components.cpp"

/**
 * @brief Bi-Connected-Components(二重頂点連結成分分解)
 * @docs docs/bi-connected-components.md
 */
template< typename T = int >
struct BiConnectedComponents : LowLink< T > {
public:
  using LowLink< T >::LowLink;
  using LowLink< T >::g;
  using LowLink< T >::ord;
  using LowLink< T >::low;

  vector< vector< Edge< T > > > bc;

  void build() override {
    LowLink< T >::build();
    used.assign(g.size(), 0);
    for(int i = 0; i < used.size(); i++) {
      if(!used[i]) dfs(i, -1);
    }
  }

  explicit BiConnectedComponents(const Graph< T > &g) : Graph< T >(g) {}

private:
  vector< int > used;
  vector< Edge< T > > tmp;

  void dfs(int idx, int par) {
    used[idx] = true;
    bool beet = false;
    for(auto &to : g[idx]) {
      if(to == par && !exchange(beet, true)) continue;
      if(!used[to] || ord[to] < ord[idx]) {
        tmp.emplace_back(to);
      }
      if(!used[to]) {
        dfs(to, idx);
        if(low[to] >= ord[idx]) {
          bc.emplace_back();
          for(;;) {
            auto e = tmp.back();
            bc.back().emplace_back(e);
            tmp.pop_back();
            if(e.idx == to.idx) break;
          }
        }
      }
    }
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

