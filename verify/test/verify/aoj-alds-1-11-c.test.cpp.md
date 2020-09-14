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


# :heavy_check_mark: test/verify/aoj-alds-1-11-c.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/aoj-alds-1-11-c.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-09-15 01:04:53+09:00


* see: <a href="http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=ALDS1_11_C">http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=ALDS1_11_C</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/graph/graph-template.cpp.html">graph/graph-template.cpp</a>
* :heavy_check_mark: <a href="../../../library/graph/shortest-path/bfs.cpp.html">BFS(幅優先探索) <small>(graph/shortest-path/bfs.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=ALDS1_11_C"

#include "../../template/template.cpp"

#include "../../graph/graph-template.cpp"

#include "../../graph/shortest-path/bfs.cpp"


int main() {
  int N, X, Y;
  cin >> N;
  Graph<> g(N);
  for(int i = 0; i < N; i++) {
    int U, K;
    cin >> U >> K;
    --U;
    for(int j = 0; j < K; j++) {
      int x;
      cin >> x;
      --x;
      g.add_directed_edge(U, x);
    }
  }
  auto d = bfs(g, 0);
  for(int i = 0; i < N; i++) {
    cout << i + 1 << " ";
    if(d[i] == numeric_limits< int >::max()) cout << -1 << "\n";
    else cout << d[i] << "\n";
  }
}


```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/aoj-alds-1-11-c.test.cpp"
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=ALDS1_11_C"

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
#line 4 "test/verify/aoj-alds-1-11-c.test.cpp"

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
#line 6 "test/verify/aoj-alds-1-11-c.test.cpp"

#line 1 "graph/shortest-path/bfs.cpp"
/**
 * @brief BFS(幅優先探索)
 */
template< typename T >
vector< T > bfs(const Graph< T > &g, int s) {
  T max_cost = 0, beet = 0;
  for(auto &es : g.g) {
    for(auto &e : es) max_cost = max(max_cost, e.cost);
  }
  ++max_cost;
  const auto INF = numeric_limits< T >::max();
  vector< T > dist(g.size(), INF);
  vector< queue< int > > ques(max_cost + 1);
  dist[s] = 0;
  ques[0].emplace(s);
  for(T cost = 0; cost <= beet; cost++) {
    auto &que = ques[cost % max_cost];
    while(!que.empty()) {
      int idx = que.front();
      que.pop();
      if(dist[idx] < cost) continue;
      for(auto &e : g.g[idx]) {
        auto next_cost = cost + e.cost;
        if(dist[e.to] <= next_cost) continue;;
        dist[e.to] = next_cost;
        beet = max(beet, dist[e.to]);
        ques[dist[e.to] % max_cost].emplace(e.to);
      }
    }
  }
  return dist;
}
#line 8 "test/verify/aoj-alds-1-11-c.test.cpp"


int main() {
  int N, X, Y;
  cin >> N;
  Graph<> g(N);
  for(int i = 0; i < N; i++) {
    int U, K;
    cin >> U >> K;
    --U;
    for(int j = 0; j < K; j++) {
      int x;
      cin >> x;
      --x;
      g.add_directed_edge(U, x);
    }
  }
  auto d = bfs(g, 0);
  for(int i = 0; i < N; i++) {
    cout << i + 1 << " ";
    if(d[i] == numeric_limits< int >::max()) cout << -1 << "\n";
    else cout << d[i] << "\n";
  }
}


```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

