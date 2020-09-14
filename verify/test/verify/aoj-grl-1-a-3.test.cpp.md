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


# :heavy_check_mark: test/verify/aoj-grl-1-a-3.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/aoj-grl-1-a-3.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-09-15 01:04:53+09:00


* see: <a href="http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_1_A">http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_1_A</a>


## Depends on

* :question: <a href="../../../library/graph/graph-template.cpp.html">graph/graph-template.cpp</a>
* :heavy_check_mark: <a href="../../../library/graph/shortest-path/dijkstra-radix-heap.cpp.html">Dijkstra-Radix-Heap(単一始点最短路) <small>(graph/shortest-path/dijkstra-radix-heap.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/structure/heap/radix-heap.cpp.html">structure/heap/radix-heap.cpp</a>
* :question: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_1_A"

#include "../../template/template.cpp"
#include "../../graph/graph-template.cpp"

#include "../../structure/heap/radix-heap.cpp"

#include "../../graph/shortest-path/dijkstra-radix-heap.cpp"

int main() {
  int V, E, R;
  cin >> V >> E >> R;
  Graph< int > g(V);
  g.read(E, 0, true, true);
  for(auto &dist : dijkstra_radix_heap(g, R)) {
    if(dist == numeric_limits< int >::max()) cout << "INF\n";
    else cout << dist << "\n";
  }
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/aoj-grl-1-a-3.test.cpp"
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_1_A"

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
#line 5 "test/verify/aoj-grl-1-a-3.test.cpp"

#line 1 "structure/heap/radix-heap.cpp"
template< typename key_t, typename val_t >
struct RadixHeap {
  static constexpr int bit = sizeof(key_t) * 8;
  array< vector< pair< key_t, val_t > >, bit > vs;

  size_t sz;
  key_t last;

  RadixHeap() : sz(0), last(0) {}

  bool empty() const { return sz == 0; }

  size_t size() const { return sz; }

  inline int getbit(int a) const {
    return a ? bit - __builtin_clz(a) : 0;
  }

  inline int getbit(int64_t a) const {
    return a ? bit - __builtin_clzll(a) : 0;
  }

  void push(const key_t &key, const val_t &val) {
    sz++;
    vs[getbit(key ^ last)].emplace_back(key, val);
  }

  pair< key_t, val_t > pop() {
    if(vs[0].empty()) {
      int idx = 1;
      while(vs[idx].empty()) idx++;
      last = min_element(vs[idx].begin(), vs[idx].end())->first;
      for(auto &p:vs[idx]) vs[getbit(p.first ^ last)].emplace_back(p);
      vs[idx].clear();
    }
    --sz;
    auto res = vs[0].back();
    vs[0].pop_back();
    return res;
  }
};
#line 7 "test/verify/aoj-grl-1-a-3.test.cpp"

#line 1 "graph/shortest-path/dijkstra-radix-heap.cpp"
/**
 * @brief Dijkstra-Radix-Heap(単一始点最短路)
 */
template< typename T >
vector< T > dijkstra_radix_heap(Graph< T > &g, int s) {
  const auto INF = numeric_limits< T >::max();
  vector< T > dist(g.size(), INF);

  using Pi = pair< T, int >;
  RadixHeap< T, int > heap;
  dist[s] = 0;
  heap.push(dist[s], s);
  while(!heap.empty()) {
    T cost;
    int idx;
    tie(cost, idx) = heap.pop();
    if(dist[idx] < cost) continue;
    for(auto &e : g.g[idx]) {
      auto next_cost = cost + e.cost;
      if(dist[e.to] <= next_cost) continue;
      dist[e.to] = next_cost;
      heap.push(dist[e.to], e.to);
    }
  }
  return dist;
}
#line 9 "test/verify/aoj-grl-1-a-3.test.cpp"

int main() {
  int V, E, R;
  cin >> V >> E >> R;
  Graph< int > g(V);
  g.read(E, 0, true, true);
  for(auto &dist : dijkstra_radix_heap(g, R)) {
    if(dist == numeric_limits< int >::max()) cout << "INF\n";
    else cout << dist << "\n";
  }
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

