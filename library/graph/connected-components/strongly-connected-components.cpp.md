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


# :heavy_check_mark: Strongly-Connected-Components(強連結成分分解) <small>(graph/connected-components/strongly-connected-components.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#3a7c46e10de1b2cce1293b2074b86f0a">graph/connected-components</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/connected-components/strongly-connected-components.cpp">View this file on GitHub</a>
    - Last commit date: 2020-09-15 01:41:10+09:00




## 概要

与えられた有向グラフを強連結成分分解する.

グラフの任意の $2$ 頂点間に有効路が存在するとき, 有向グラフが強連結であるとよぶ. 強連結成分は, 極大で強連結な部分グラフである.

適当な頂点からDFSをして, 帰りがけ順に頂点を列挙することを, 未訪問の頂点がある間繰り返す. 次に辺をすべて逆向きにしたグラフについて, 列挙した頂点の逆順にDFS する. $1$ 回の DFS で到達できた頂点が $1$ つの強連結成分となる.

強連結成分を縮約後の頂点とそれらを結ぶ辺からなるグラフはDAGになっている.

* `build()`: 強連結成分分解する. `dag` には縮約後の頂点と辺からなるDAGが格納される. `comp` には各頂点が属する強連結成分の頂点番号が格納される. `group` には各強連結成分について, それに属する頂点が格納される.

## 計算量

* $O(E + V)$


## Depends on

* :heavy_check_mark: <a href="../graph-template.cpp.html">graph/graph-template.cpp</a>


## Required by

* :heavy_check_mark: <a href="../others/two-satisfiability.cpp.html">2-SAT <small>(graph/others/two-satisfiability.cpp)</small></a>


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-grl-3-c.test.cpp.html">test/verify/aoj-grl-3-c.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-scc.test.cpp.html">test/verify/yosupo-scc.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-two-sat.test.cpp.html">test/verify/yosupo-two-sat.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#include "../graph-template.cpp"

/**
 * @brief Strongly-Connected-Components(強連結成分分解)
 * @docs docs/strongly-connected-components.md
 */
template< typename T = int >
struct StronglyConnectedComponents : Graph< T > {
public:
  using Graph< T >::Graph;
  using Graph< T >::g;
  vector< int > comp;
  Graph< T > dag;
  vector< vector< int > > group;

  void build() {
    rg = Graph< T >(g.size());
    for(int i = 0; i < g.size(); i++) {
      for(auto &e : g[i]) {
        rg.add_directed_edge(e.to, e.from, e.cost);
      }
    }
    comp.assign(g.size(), -1);
    used.assign(g.size(), 0);
    for(int i = 0; i < g.size(); i++) dfs(i);
    reverse(begin(order), end(order));
    int ptr = 0;
    for(int i : order) if(comp[i] == -1) rdfs(i, ptr), ptr++;
    dag = Graph< T >(ptr);
    for(int i = 0; i < g.size(); i++) {
      for(auto &e : g[i]) {
        int x = comp[e.from], y = comp[e.to];
        if(x == y) continue;
        dag.add_directed_edge(x, y, e.cost);
      }
    }
    group.resize(ptr);
    for(int i = 0; i < g.size(); i++) {
      group[comp[i]].emplace_back(i);
    }
  }

  int operator[](int k) const {
    return comp[k];
  }

private:
  vector< int > order, used;
  Graph< T > rg;

  void dfs(int idx) {
    if(exchange(used[idx], true)) return;
    for(auto &to : g[idx]) dfs(to);
    order.push_back(idx);
  }

  void rdfs(int idx, int cnt) {
    if(comp[idx] != -1) return;
    comp[idx] = cnt;
    for(auto &to : rg.g[idx]) rdfs(to, cnt);
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
#line 2 "graph/connected-components/strongly-connected-components.cpp"

/**
 * @brief Strongly-Connected-Components(強連結成分分解)
 * @docs docs/strongly-connected-components.md
 */
template< typename T = int >
struct StronglyConnectedComponents : Graph< T > {
public:
  using Graph< T >::Graph;
  using Graph< T >::g;
  vector< int > comp;
  Graph< T > dag;
  vector< vector< int > > group;

  void build() {
    rg = Graph< T >(g.size());
    for(int i = 0; i < g.size(); i++) {
      for(auto &e : g[i]) {
        rg.add_directed_edge(e.to, e.from, e.cost);
      }
    }
    comp.assign(g.size(), -1);
    used.assign(g.size(), 0);
    for(int i = 0; i < g.size(); i++) dfs(i);
    reverse(begin(order), end(order));
    int ptr = 0;
    for(int i : order) if(comp[i] == -1) rdfs(i, ptr), ptr++;
    dag = Graph< T >(ptr);
    for(int i = 0; i < g.size(); i++) {
      for(auto &e : g[i]) {
        int x = comp[e.from], y = comp[e.to];
        if(x == y) continue;
        dag.add_directed_edge(x, y, e.cost);
      }
    }
    group.resize(ptr);
    for(int i = 0; i < g.size(); i++) {
      group[comp[i]].emplace_back(i);
    }
  }

  int operator[](int k) const {
    return comp[k];
  }

private:
  vector< int > order, used;
  Graph< T > rg;

  void dfs(int idx) {
    if(exchange(used[idx], true)) return;
    for(auto &to : g[idx]) dfs(to);
    order.push_back(idx);
  }

  void rdfs(int idx, int cnt) {
    if(comp[idx] != -1) return;
    comp[idx] = cnt;
    for(auto &to : rg.g[idx]) rdfs(to, cnt);
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

