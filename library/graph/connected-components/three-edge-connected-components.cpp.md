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


# :heavy_check_mark: Three-Edge-Connected-Components(三重辺連結成分分解) <small>(graph/connected-components/three-edge-connected-components.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#3a7c46e10de1b2cce1293b2074b86f0a">graph/connected-components</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/connected-components/three-edge-connected-components.cpp">View this file on GitHub</a>
    - Last commit date: 2020-09-15 01:41:10+09:00




## Depends on

* :heavy_check_mark: <a href="incremental-bridge-connectivity.cpp.html">Incremental-Bridge-Connectivity <small>(graph/connected-components/incremental-bridge-connectivity.cpp)</small></a>
* :heavy_check_mark: <a href="../graph-template.cpp.html">graph/graph-template.cpp</a>
* :heavy_check_mark: <a href="../../structure/union-find/union-find.cpp.html">Union-Find <small>(structure/union-find/union-find.cpp)</small></a>


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-three-edge-connected-components.test.cpp.html">test/verify/yosupo-three-edge-connected-components.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#include "../graph-template.cpp"
#include "incremental-bridge-connectivity.cpp"

/**
 * @brief Three-Edge-Connected-Components(三重辺連結成分分解)
 */
template< typename T = int >
struct ThreeEdgeConnectedComponents : Graph< T > {
public:
  using Graph< T >::Graph;
  using Graph< T >::g;
  vector< vector< int > > group;

  void build() {
    uf = UnionFind(g.size());
    bcc = IncrementalBridgeConnectivity(g.size());
    used.assign(g.size(), 0);
    in.assign(g.size(), 0);
    out.assign(g.size(), 0);
    deg.assign(g.size(), 0);
    low.assign(g.size(), g.size());
    for(int from = 0; from < g.size(); from++) {
      for(auto &to : g[from]) {
        if(from < to) bcc.add_edge(from, to);
      }
    }
    int cnt = 0;
    for(int i = 0; i < g.size(); i++) {
      if(used[i]) continue;
      vector< int > tmp;
      dfs(i, -1, tmp, cnt);
      cnt++;
    }
    vector< int > id(g.size(), -1);
    cnt = 0;
    for(int i = 0; i < g.size(); i++) {
      if(id[uf.find(i)] == -1) id[uf.find(i)] = cnt++;
    }
    group.resize(cnt);
    for(int i = 0; i < g.size(); i++) {
      group[id[uf.find(i)]].emplace_back(i);
    }
  }

  int operator[](const int &k) {
    return uf.find(k);
  }

private:
  vector< int > used;
  vector< int > in, out, low, deg;
  IncrementalBridgeConnectivity bcc;
  UnionFind uf;

  void absorb(vector< int > &path, int v, int w = -1) {
    while(!path.empty()) {
      int x = path.back();
      if(w != -1 && (in[x] > in[w] or in[w] >= out[x])) break;
      path.pop_back();
      uf.unite(v, x);
      deg[v] += deg[x] - 2;
    }
  }

  void dfs(int idx, int p, vector< int > &path, int &k) {
    used[idx] = 1;
    in[idx] = low[idx] = k++;
    for(auto &to : g[idx]) {
      if(idx == to || bcc.find(idx) != bcc.find(to)) continue;
      deg[idx]++;
      if(to == p) {
        p = -1;
        continue;
      }
      if(used[to]) {
        if(in[idx] > in[to]) {
          if(in[to] < low[idx]) {
            low[idx] = in[to];
            absorb(path, idx);
          }
        } else {
          deg[idx] -= 2;
          absorb(path, idx, to);
        }
      } else {
        vector< int > ps;
        dfs(to, idx, ps, k);
        if(deg[to] == 2) ps.pop_back();
        if(low[to] < low[idx]) {
          low[idx] = low[to];
          absorb(path, idx);
          path = ps;
        } else {
          absorb(ps, idx);
        }
      }
    }
    out[idx] = k;
    path.push_back(idx);
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
#line 1 "structure/union-find/union-find.cpp"
/**
 * @brief Union-Find
 * @docs docs/union-find.md
 */
struct UnionFind {
  vector< int > data;

  UnionFind() = default;

  explicit UnionFind(size_t sz) : data(sz, -1) {}

  bool unite(int x, int y) {
    x = find(x), y = find(y);
    if(x == y) return false;
    if(data[x] > data[y]) swap(x, y);
    data[x] += data[y];
    data[y] = x;
    return true;
  }

  int find(int k) {
    if(data[k] < 0) return (k);
    return data[k] = find(data[k]);
  }

  int size(int k) {
    return -data[find(k)];
  }

  bool same(int x, int y) {
    return find(x) == find(y);
  }
};
#line 2 "graph/connected-components/incremental-bridge-connectivity.cpp"

/**
 * @brief Incremental-Bridge-Connectivity
 * @docs docs/incremental-bridge-connectivity.md
 * @see https://scrapbox.io/data-structures/Incremental_Bridge-Connectivity
 */
struct IncrementalBridgeConnectivity {
private:
  UnionFind cc, bcc;
  vector< int > bbf;
  size_t bridge;

  int size() {
    return bbf.size();
  }

  int par(int x) {
    return bbf[x] == size() ? size() : bcc.find(bbf[x]);
  }

  int lca(int x, int y) {
    unordered_set< int > used;
    for(;;) {
      if(x != size()) {
        if(!used.insert(x).second) return x;
        x = par(x);
      }
      swap(x, y);
    }
  }

  void compress(int x, int y) {
    while(bcc.find(x) != bcc.find(y)) {
      int nxt = par(x);
      bbf[x] = bbf[y];
      bcc.unite(x, y);
      x = nxt;
      --bridge;
    }
  }

  void link(int x, int y) {
    int v = x, pre = y;
    while(v != size()) {
      int nxt = par(v);
      bbf[v] = pre;
      pre = v;
      v = nxt;
    }
  }

public:
  IncrementalBridgeConnectivity() = default;

  explicit IncrementalBridgeConnectivity(int sz) : cc(sz), bcc(sz), bbf(sz, sz), bridge(0) {}

  int find(int k) {
    return bcc.find(k);
  }

  size_t bridge_size() const {
    return bridge;
  }

  void add_edge(int x, int y) {
    x = bcc.find(x);
    y = bcc.find(y);
    if(cc.find(x) == cc.find(y)) {
      int w = lca(x, y);
      compress(x, w);
      compress(y, w);
    } else {
      if(cc.size(x) > cc.size(y)) swap(x, y);
      link(x, y);
      cc.unite(x, y);
      ++bridge;
    }
  }
};
#line 3 "graph/connected-components/three-edge-connected-components.cpp"

/**
 * @brief Three-Edge-Connected-Components(三重辺連結成分分解)
 */
template< typename T = int >
struct ThreeEdgeConnectedComponents : Graph< T > {
public:
  using Graph< T >::Graph;
  using Graph< T >::g;
  vector< vector< int > > group;

  void build() {
    uf = UnionFind(g.size());
    bcc = IncrementalBridgeConnectivity(g.size());
    used.assign(g.size(), 0);
    in.assign(g.size(), 0);
    out.assign(g.size(), 0);
    deg.assign(g.size(), 0);
    low.assign(g.size(), g.size());
    for(int from = 0; from < g.size(); from++) {
      for(auto &to : g[from]) {
        if(from < to) bcc.add_edge(from, to);
      }
    }
    int cnt = 0;
    for(int i = 0; i < g.size(); i++) {
      if(used[i]) continue;
      vector< int > tmp;
      dfs(i, -1, tmp, cnt);
      cnt++;
    }
    vector< int > id(g.size(), -1);
    cnt = 0;
    for(int i = 0; i < g.size(); i++) {
      if(id[uf.find(i)] == -1) id[uf.find(i)] = cnt++;
    }
    group.resize(cnt);
    for(int i = 0; i < g.size(); i++) {
      group[id[uf.find(i)]].emplace_back(i);
    }
  }

  int operator[](const int &k) {
    return uf.find(k);
  }

private:
  vector< int > used;
  vector< int > in, out, low, deg;
  IncrementalBridgeConnectivity bcc;
  UnionFind uf;

  void absorb(vector< int > &path, int v, int w = -1) {
    while(!path.empty()) {
      int x = path.back();
      if(w != -1 && (in[x] > in[w] or in[w] >= out[x])) break;
      path.pop_back();
      uf.unite(v, x);
      deg[v] += deg[x] - 2;
    }
  }

  void dfs(int idx, int p, vector< int > &path, int &k) {
    used[idx] = 1;
    in[idx] = low[idx] = k++;
    for(auto &to : g[idx]) {
      if(idx == to || bcc.find(idx) != bcc.find(to)) continue;
      deg[idx]++;
      if(to == p) {
        p = -1;
        continue;
      }
      if(used[to]) {
        if(in[idx] > in[to]) {
          if(in[to] < low[idx]) {
            low[idx] = in[to];
            absorb(path, idx);
          }
        } else {
          deg[idx] -= 2;
          absorb(path, idx, to);
        }
      } else {
        vector< int > ps;
        dfs(to, idx, ps, k);
        if(deg[to] == 2) ps.pop_back();
        if(low[to] < low[idx]) {
          low[idx] = low[to];
          absorb(path, idx);
          path = ps;
        } else {
          absorb(ps, idx);
        }
      }
    }
    out[idx] = k;
    path.push_back(idx);
  }
};


```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

