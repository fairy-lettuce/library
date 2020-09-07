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


# :heavy_check_mark: test/verify/yukicoder-1069.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yukicoder-1069.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-22 20:09:30+09:00


* see: <a href="https://yukicoder.me/problems/no/1069">https://yukicoder.me/problems/no/1069</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/graph/graph-template.cpp.html">graph/graph-template.cpp</a>
* :heavy_check_mark: <a href="../../../library/graph/shortest-path/k-shortest-path.cpp.html">K-Shortest-Path <small>(graph/shortest-path/k-shortest-path.cpp)</small></a>
* :question: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define ERROR "1e-4"
#define PROBLEM "https://yukicoder.me/problems/no/1069"

#include "../../template/template.cpp"

#include "../../graph/graph-template.cpp"
#include "../../graph/shortest-path/k-shortest-path.cpp"

int main() {
  int N, M, K;
  cin >> N >> M >> K;
  int X, Y;
  cin >> X >> Y;
  --X, --Y;
  vector< int > P(N), Q(N);
  for(int i = 0; i < N; i++) {
    cin >> P[i] >> Q[i];
  }
  Graph< double > g(N);
  vector< int > x(M * 2), y(M * 2);
  for(int i = 0; i < M; i++) {
    int a, b;
    cin >> a >> b;
    --a, --b;
    g.add_directed_edge(a, b, hypot(P[a] - P[b], Q[a] - Q[b]));
    x[i] = a, y[i] = b;
  }
  for(int i = 0; i < M; i++) {
    int a = x[i], b = y[i];
    x[i + M] = b, y[i + M] = a;
    g.add_directed_edge(b, a, hypot(P[a] - P[b], Q[a] - Q[b]));
  }
  auto ans = k_shortest_path(g, X, Y, K);
  for(int i = 0; i < K; i++) {
    if(i < ans.size()) cout << ans[i].first << "\n";
    else cout << -1 << "\n";
  }
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yukicoder-1069.test.cpp"
#define ERROR "1e-4"
#define PROBLEM "https://yukicoder.me/problems/no/1069"

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
#line 5 "test/verify/yukicoder-1069.test.cpp"

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
#line 1 "graph/shortest-path/k-shortest-path.cpp"
/**
 * @brief K-Shortest-Path
 * @docs docs/k-shortest-path.md
 * @see https://qiita.com/nariaki3551/items/821dc6ffdc552d3d5f22
 */
template< typename T >
vector< pair< T, vector< int > > > k_shortest_path(const Graph< T > &g, int s, int t, int k) {
  assert(s != t);
  int N = (int) g.size();
  int M = 0;
  for(int i = 0; i < N; i++) M += g.g[i].size();
  vector< int > latte(M), malta(M);
  vector< T > cost(M);
  for(int i = 0; i < N; i++) {
    for(auto &e : g.g[i]) {
      latte[e.idx] = i;
      malta[e.idx] = e.to;
      cost[e.idx] = e.cost;
    }
  }
  const auto INF = numeric_limits< T >::max();
  vector< int > dame(M, -1);
  int timestamp = 0;
  auto shortest_path = [&](vector< T > &dist, vector< int > &from, vector< int > &id, int st) {
    using Pi = pair< T, int >;
    priority_queue< Pi, vector< Pi >, greater<> > que;
    que.emplace(dist[st], st);
    while(!que.empty()) {
      T cost;
      int idx;
      tie(cost, idx) = que.top();
      que.pop();
      if(dist[idx] < cost) continue;
      if(idx == t) return;
      for(auto &e : g.g[idx]) {
        auto next_cost = cost + e.cost;
        if(dist[e.to] <= next_cost) continue;
        if(dame[e.idx] == timestamp) continue;
        dist[e.to] = next_cost;
        from[e.to] = idx;
        id[e.to] = e.idx;
        que.emplace(dist[e.to], e.to);
      }
    }
  };
  auto restore = [](const vector< int > &es, const vector< int > &vs, int from, int to) {
    vector< int > tap;
    while(to != from) {
      tap.emplace_back(es[to]);
      to = vs[to];
    }
    reverse(begin(tap), end(tap));
    return tap;
  };

  vector< T > dist(g.size(), INF);
  vector< int > from(g.size(), -1), id(g.size(), -1);
  dist[s] = 0;
  shortest_path(dist, from, id, s);
  if(dist[t] == INF) return {};

  vector< pair< T, vector< int > > > A;
  set< pair< T, vector< int > > > B;
  A.emplace_back(dist[t], restore(id, from, s, t));

  for(int i = 1; i < k; i++) {
    dist.assign(g.size(), INF);
    from.assign(g.size(), -1);
    id.assign(g.size(), -1);
    dist[s] = 0;
    vector< int > candidate(A.size());
    iota(begin(candidate), end(candidate), 0);
    auto &last_path = A.back().second;
    int cur = s;
    for(int j = 0; j < last_path.size(); j++) {
      for(auto &k : candidate) {
        if(j < A[k].second.size()) dame[A[k].second[j]] = timestamp;
      }
      vector< T > dist2{dist};
      vector< int > from2{from}, id2{id};
      shortest_path(dist2, from2, id2, cur);
      ++timestamp;
      if(dist2[t] != INF) {
        auto path = restore(id2, from2, s, t);
        bool ok = true;
        for(auto &p : candidate) {
          if(path == A[p].second) {
            ok = false;
            break;
          }
        }
        if(ok) B.emplace(dist2[t], path);
      }
      vector< int > accept;
      for(auto &k : candidate) {
        if(j < A[k].second.size() && A[k].second[j] == last_path[j]) {
          accept.emplace_back(k);
        }
      }
      dist[malta[last_path[j]]] = dist[latte[last_path[j]]] + cost[last_path[j]];
      from[malta[last_path[j]]] = latte[last_path[j]];
      id[malta[last_path[j]]] = last_path[j];
      cur = malta[last_path[j]];
      candidate = move(accept);
    }
    if(B.size()) {
      A.emplace_back(*B.begin());
      B.erase(B.begin());
    }
  }
  return A;
}
#line 8 "test/verify/yukicoder-1069.test.cpp"

int main() {
  int N, M, K;
  cin >> N >> M >> K;
  int X, Y;
  cin >> X >> Y;
  --X, --Y;
  vector< int > P(N), Q(N);
  for(int i = 0; i < N; i++) {
    cin >> P[i] >> Q[i];
  }
  Graph< double > g(N);
  vector< int > x(M * 2), y(M * 2);
  for(int i = 0; i < M; i++) {
    int a, b;
    cin >> a >> b;
    --a, --b;
    g.add_directed_edge(a, b, hypot(P[a] - P[b], Q[a] - Q[b]));
    x[i] = a, y[i] = b;
  }
  for(int i = 0; i < M; i++) {
    int a = x[i], b = y[i];
    x[i + M] = b, y[i + M] = a;
    g.add_directed_edge(b, a, hypot(P[a] - P[b], Q[a] - Q[b]));
  }
  auto ans = k_shortest_path(g, X, Y, K);
  for(int i = 0; i < K; i++) {
    if(i < ans.size()) cout << ans[i].first << "\n";
    else cout << -1 << "\n";
  }
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

