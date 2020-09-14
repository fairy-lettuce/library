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


# :x: test/verify/yosupo-two-edge-connected-components.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yosupo-two-edge-connected-components.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-09-15 01:04:53+09:00


* see: <a href="https://judge.yosupo.jp/problem/two_edge_connected_components">https://judge.yosupo.jp/problem/two_edge_connected_components</a>


## Depends on

* :x: <a href="../../../library/graph/connected-components/two-edge-connected-components.cpp.html">Two-Edge-Connected-Components(二重辺連結成分分解) <small>(graph/connected-components/two-edge-connected-components.cpp)</small></a>
* :question: <a href="../../../library/graph/graph-template.cpp.html">graph/graph-template.cpp</a>
* :question: <a href="../../../library/graph/others/low-link.cpp.html">Low-Link(橋/関節点) <small>(graph/others/low-link.cpp)</small></a>
* :question: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://judge.yosupo.jp/problem/two_edge_connected_components"

#include "../../template/template.cpp"

#include "../../graph/connected-components/two-edge-connected-components.cpp"

int main() {
  int N, M;
  cin >> N >> M;
  TwoEdgeConnectedComponents<> g(N);
  g.read(M, 0);
  g.build();
  cout << g.group.size() << "\n";
  for(auto &p : g.group) {
    cout << p.size() << " " << p << "\n";
  }
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yosupo-two-edge-connected-components.test.cpp"
#define PROBLEM "https://judge.yosupo.jp/problem/two_edge_connected_components"

#line 1 "template/template.cpp"
#include<bits/stdc++.h>

using namespace std;

using int64 = long long;
const int mod = 1e9 + 7;

const int64 infll = (1LL << 62) - 1;
const int inf = (1 << 30) - 1;

struct IoSetup {
  IoSetup() {
    cin.tie(nullptr);
    ios::sync_with_stdio(false);
    cout << fixed << setprecision(10);
    cerr << fixed << setprecision(10);
  }
} iosetup;


template< typename T1, typename T2 >
ostream &operator<<(ostream &os, const pair< T1, T2 >& p) {
  os << p.first << " " << p.second;
  return os;
}

template< typename T1, typename T2 >
istream &operator>>(istream &is, pair< T1, T2 > &p) {
  is >> p.first >> p.second;
  return is;
}

template< typename T >
ostream &operator<<(ostream &os, const vector< T > &v) {
  for(int i = 0; i < (int) v.size(); i++) {
    os << v[i] << (i + 1 != v.size() ? " " : "");
  }
  return os;
}

template< typename T >
istream &operator>>(istream &is, vector< T > &v) {
  for(T &in : v) is >> in;
  return is;
}

template< typename T1, typename T2 >
inline bool chmax(T1 &a, T2 b) { return a < b && (a = b, true); }

template< typename T1, typename T2 >
inline bool chmin(T1 &a, T2 b) { return a > b && (a = b, true); }

template< typename T = int64 >
vector< T > make_v(size_t a) {
  return vector< T >(a);
}

template< typename T, typename... Ts >
auto make_v(size_t a, Ts... ts) {
  return vector< decltype(make_v< T >(ts...)) >(a, make_v< T >(ts...));
}

template< typename T, typename V >
typename enable_if< is_class< T >::value == 0 >::type fill_v(T &t, const V &v) {
  t = v;
}

template< typename T, typename V >
typename enable_if< is_class< T >::value != 0 >::type fill_v(T &t, const V &v) {
  for(auto &e : t) fill_v(e, v);
}

template< typename F >
struct FixPoint : F {
  FixPoint(F &&f) : F(forward< F >(f)) {}
 
  template< typename... Args >
  decltype(auto) operator()(Args &&... args) const {
    return F::operator()(*this, forward< Args >(args)...);
  }
};
 
template< typename F >
inline decltype(auto) MFP(F &&f) {
  return FixPoint< F >{forward< F >(f)};
}
#line 4 "test/verify/yosupo-two-edge-connected-components.test.cpp"

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
#line 2 "graph/connected-components/two-edge-connected-components.cpp"

/**
 * @brief Two-Edge-Connected-Components(二重辺連結成分分解)
 * @docs docs/two-edge-connected-components.md
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
#line 6 "test/verify/yosupo-two-edge-connected-components.test.cpp"

int main() {
  int N, M;
  cin >> N >> M;
  TwoEdgeConnectedComponents<> g(N);
  g.read(M, 0);
  g.build();
  cout << g.group.size() << "\n";
  for(auto &p : g.group) {
    cout << p.size() << " " << p << "\n";
  }
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

