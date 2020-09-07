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


# :heavy_check_mark: test/verify/yosupo-k-shortest-walk.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yosupo-k-shortest-walk.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-21 01:30:35+09:00


* see: <a href="https://judge.yosupo.jp/problem/k_shortest_walk">https://judge.yosupo.jp/problem/k_shortest_walk</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/graph/graph-template.cpp.html">graph/graph-template.cpp</a>
* :heavy_check_mark: <a href="../../../library/graph/shortest-path/dijkstra.cpp.html">Dijkstra(単一始点最短路) <small>(graph/shortest-path/dijkstra.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/graph/shortest-path/k-shortest-walk.cpp.html">K-Shortest-Walk <small>(graph/shortest-path/k-shortest-walk.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/structure/heap/leftist-heap.cpp.html">Leftist-Heap <small>(structure/heap/leftist-heap.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/structure/heap/persistent-leftist-heap.cpp.html">Persistent-Leftist-Heap <small>(structure/heap/persistent-leftist-heap.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://judge.yosupo.jp/problem/k_shortest_walk"

#include "../../template/template.cpp"

#include "../../graph/graph-template.cpp"
#include "../../graph/shortest-path/dijkstra.cpp"

#include "../../structure/heap/leftist-heap.cpp"
#include "../../structure/heap/persistent-leftist-heap.cpp"
#include "../../graph/shortest-path/k-shortest-walk.cpp"

int main() {
  int N, M, S, T, K;
  cin >> N >> M >> S >> T >> K;
  Graph< int64 > g(N);
  g.read(M, 0, true, true);
  auto ret = k_shortest_walk(g, S, T, K);
  for(int i = 0; i < K; i++) {
    if(i >= ret.size()) cout << -1 << "\n";
    else cout << ret[i] << "\n";
  }
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yosupo-k-shortest-walk.test.cpp"
#define PROBLEM "https://judge.yosupo.jp/problem/k_shortest_walk"

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
#line 4 "test/verify/yosupo-k-shortest-walk.test.cpp"

#line 1 "graph/graph-template.cpp"
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
#line 1 "graph/shortest-path/dijkstra.cpp"
/**
 * @brief Dijkstra(単一始点最短路)
 * @docs docs/dijkstra.md
 */
template< typename T >
struct ShortestPath {
  vector< T > dist;
  vector< int > from, id;
};

template< typename T >
ShortestPath< T > dijkstra(const Graph< T > &g, int s) {
  const auto INF = numeric_limits< T >::max();
  vector< T > dist(g.size(), INF);
  vector< int > from(g.size(), -1), id(g.size(), -1);
  using Pi = pair< T, int >;
  priority_queue< Pi, vector< Pi >, greater<> > que;
  dist[s] = 0;
  que.emplace(dist[s], s);
  while(!que.empty()) {
    T cost;
    int idx;
    tie(cost, idx) = que.top();
    que.pop();
    if(dist[idx] < cost) continue;
    for(auto &e : g.g[idx]) {
      auto next_cost = cost + e.cost;
      if(dist[e.to] <= next_cost) continue;
      dist[e.to] = next_cost;
      from[e.to] = idx;
      id[e.to] = e.idx;
      que.emplace(dist[e.to], e.to);
    }
  }
  return {dist, from, id};
}
#line 7 "test/verify/yosupo-k-shortest-walk.test.cpp"

#line 1 "structure/heap/leftist-heap.cpp"
/**
 * @brief Leftist-Heap
 */
template< typename T, bool isMin = true >
struct LeftistHeap {
  struct Node {
    Node *l, *r;
    int s;
    T key;
    int idx;

    explicit Node(const T &key, int idx) : key(key), s(1), l(nullptr), r(nullptr), idx(idx) {}
  };

  LeftistHeap() = default;

  virtual Node *clone(Node *t) {
    return t;
  }

  Node *alloc(const T &key, int idx = -1) {
    return new Node(key, idx);
  }

  Node *meld(Node *a, Node *b) {
    if(!a || !b) return a ? a : b;
    if((a->key < b->key) ^ isMin) swap(a, b);
    a = clone(a);
    a->r = meld(a->r, b);
    if(!a->l || a->l->s < a->r->s) swap(a->l, a->r);
    a->s = (a->r ? a->r->s : 0) + 1;
    return a;
  }

  Node *push(Node *t, const T &key, int idx = -1) {
    return meld(t, alloc(key, idx));
  }

  Node *pop(Node *t) {
    assert(t != nullptr);
    return meld(t->l, t->r);
  }

  Node *make_root() {
    return nullptr;
  }
};
#line 1 "structure/heap/persistent-leftist-heap.cpp"
/**
 * @brief Persistent-Leftist-Heap
 */
template< typename T, bool isMin = true >
struct PersistentLeftistHeap : LeftistHeap< T, isMin > {
  using Node = typename LeftistHeap< T, isMin >::Node;

  Node *clone(Node *t) override {
    return new Node(*t);
  }
};
#line 1 "graph/shortest-path/k-shortest-walk.cpp"
/**
 * @brief K-Shortest-Walk
 * @docs docs/k-shortest-walk.md
 * @see https://qiita.com/hotman78/items/42534a01c4bd05ed5e1e
 */
template< typename T >
vector< T > k_shortest_walk(const Graph< T > &g, int s, int t, int k) {
  int N = (int) g.size();
  Graph< T > rg(N);
  for(int i = 0; i < N; i++) {
    for(auto &e : g.g[i]) rg.add_directed_edge(e.to, i, e.cost);
  }
  auto dist = dijkstra(rg, t);
  if(dist.from[s] == -1) return {};
  auto &p = dist.dist;
  vector< vector< int > > ch(N);
  for(int i = 0; i < N; i++) {
    if(dist.from[i] >= 0) ch[dist.from[i]].emplace_back(i);
  }
  using PHeap = PersistentLeftistHeap< T >;
  using Node = typename PHeap::Node;
  PHeap heap;
  vector< Node * > h(N, heap.make_root());
  {
    queue< int > que;
    que.emplace(t);
    while(!que.empty()) {
      int idx = que.front();
      que.pop();
      if(dist.from[idx] >= 0) {
        h[idx] = heap.meld(h[idx], h[dist.from[idx]]);
      }
      bool used = true;
      for(auto &e : g.g[idx]) {
        if(e.to != t && dist.from[e.to] == -1) continue;
        if(used && dist.from[idx] == e.to && p[e.to] + e.cost == p[idx]) {
          used = false;
          continue;
        }
        h[idx] = heap.push(h[idx], e.cost - p[idx] + p[e.to], e.to);
      }
      for(auto &to : ch[idx]) que.emplace(to);
    }
  }
  using pi = pair< T, Node * >;
  auto comp = [](const pi &x, const pi &y) { return x.first > y.first; };
  priority_queue< pi, vector< pi >, decltype(comp) > que(comp);
  Node *root = heap.make_root();
  root = heap.push(root, p[s], s);
  que.emplace(p[s], root);
  vector< T > ans;
  while(!que.empty()) {
    T cost;
    Node *cur;
    tie(cost, cur) = que.top();
    que.pop();
    ans.emplace_back(cost);
    if(ans.size() == k) break;
    if(cur->l) que.emplace(cost + cur->l->key - cur->key, cur->l);
    if(cur->r) que.emplace(cost + cur->r->key - cur->key, cur->r);
    if(h[cur->idx]) que.emplace(cost + h[cur->idx]->key, h[cur->idx]);
  }
  return ans;
}
#line 11 "test/verify/yosupo-k-shortest-walk.test.cpp"

int main() {
  int N, M, S, T, K;
  cin >> N >> M >> S >> T >> K;
  Graph< int64 > g(N);
  g.read(M, 0, true, true);
  auto ret = k_shortest_walk(g, S, T, K);
  for(int i = 0; i < K; i++) {
    if(i >= ret.size()) cout << -1 << "\n";
    else cout << ret[i] << "\n";
  }
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

