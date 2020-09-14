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


# :heavy_check_mark: test/verify/yosupo-bipartitematching.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yosupo-bipartitematching.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-10 19:29:34+09:00


* see: <a href="https://judge.yosupo.jp/problem/bipartitematching">https://judge.yosupo.jp/problem/bipartitematching</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/graph/flow/bipartite-flow.cpp.html">Bipartite-Flow(二部グラフのフロー) <small>(graph/flow/bipartite-flow.cpp)</small></a>
* :question: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://judge.yosupo.jp/problem/bipartitematching"

#include "../../template/template.cpp"

#include "../../graph/flow/bipartite-flow.cpp"

int main() {
  int L, R, M;
  cin >> L >> R >> M;
  BipartiteFlow flow(L, R);
  for(int i = 0; i < M; i++) {
    int a, b;
    cin >> a >> b;
    flow.add_edge(a, b);
  }
  auto es = flow.max_matching();
  cout << es.size() << "\n";
  for(auto &p : es) cout << p.first << " " << p.second << "\n";
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yosupo-bipartitematching.test.cpp"
#define PROBLEM "https://judge.yosupo.jp/problem/bipartitematching"

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
#line 4 "test/verify/yosupo-bipartitematching.test.cpp"

#line 1 "graph/flow/bipartite-flow.cpp"
/**
 * @brief Bipartite-Flow(二部グラフのフロー)
 * @docs docs/bipartite-flow.md
 */
struct BipartiteFlow {
  size_t n, m, time_stamp;
  vector< vector< int > > g, rg;
  vector< int > match_l, match_r, dist, used, alive;
  bool matched;

public:
  explicit BipartiteFlow(size_t n, size_t m) :
      n(n), m(m), g(n), rg(m), match_l(n, -1), match_r(m, -1), used(n), alive(n, 1), time_stamp(0), matched(false) {}

  void add_edge(int u, int v) {
    g[u].push_back(v);
    rg[v].emplace_back(u);
  }

  vector< pair< int, int > > max_matching() {
    matched = true;
    for(;;) {
      build_augment_path();
      ++time_stamp;
      int flow = 0;
      for(int i = 0; i < n; i++) {
        if(match_l[i] == -1) flow += find_min_dist_augment_path(i);
      }
      if(flow == 0) break;
    }
    vector< pair< int, int > > ret;
    for(int i = 0; i < n; i++) {
      if(match_l[i] >= 0) ret.emplace_back(i, match_l[i]);
    }
    return ret;
  }

  /* http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=0334 */
  vector< pair< int, int > > lex_max_matching() {
    if(!matched) max_matching();
    for(auto &vs : g) sort(begin(vs), end(vs));
    vector< pair< int, int > > es;
    for(int i = 0; i < n; i++) {
      if(match_l[i] == -1 || alive[i] == 0) {
        continue;
      }
      match_r[match_l[i]] = -1;
      match_l[i] = -1;
      ++time_stamp;
      find_augment_path(i);
      alive[i] = 0;
      es.emplace_back(i, match_l[i]);
    }
    return es;
  }

  vector< int > min_vertex_cover() {
    auto visited = find_residual_path();
    vector< int > ret;
    for(int i = 0; i < n + m; i++) {
      if(visited[i] ^ (i < n)) {
        ret.emplace_back(i);
      }
    }
    return ret;
  }

  /* https://atcoder.jp/contests/utpc2013/tasks/utpc2013_11 */
  vector< int > lex_min_vertex_cover(const vector< int > &ord) {
    assert(ord.size() == n + m);
    auto res = build_risidual_graph();
    vector< vector< int > > r_res(n + m + 2);
    for(int i = 0; i < n + m + 2; i++) {
      for(auto &j : res[i]) r_res[j].emplace_back(i);
    }
    queue< int > que;
    vector< int > visited(n + m + 2, -1);
    auto expand_left = [&](int t) {
      if(visited[t] != -1) return;
      que.emplace(t);
      visited[t] = 1;
      while(!que.empty()) {
        int idx = que.front();
        que.pop();
        for(auto &to : r_res[idx]) {
          if(visited[to] != -1) continue;
          visited[to] = 1;
          que.emplace(to);
        }
      }
    };
    auto expand_right = [&](int t) {
      if(visited[t] != -1) return;
      que.emplace(t);
      visited[t] = 0;
      while(!que.empty()) {
        int idx = que.front();
        que.pop();
        for(auto &to : res[idx]) {
          if(visited[to] != -1) continue;
          visited[to] = 0;
          que.emplace(to);
        }
      }
    };
    expand_right(n + m);
    expand_left(n + m + 1);
    vector< int > ret;
    for(auto &t : ord) {
      if(t < n) {
        expand_left(t);
        if(visited[t] & 1) ret.emplace_back(t);
      } else {
        expand_right(t);
        if(~visited[t] & 1) ret.emplace_back(t);
      }
    }
    return ret;
  }


  vector< int > max_independent_set() {
    auto visited = find_residual_path();
    vector< int > ret;
    for(int i = 0; i < n + m; i++) {
      if(visited[i] ^ (i >= n)) {
        ret.emplace_back(i);
      }
    }
    return ret;
  }

  vector< pair< int, int > > min_edge_cover() {
    auto es = max_matching();
    for(int i = 0; i < n; i++) {
      if(match_l[i] >= 0) {
        continue;
      }
      if(g[i].empty()) {
        return {};
      }
      es.emplace_back(i, g[i][0]);
    }
    for(int i = 0; i < m; i++) {
      if(match_r[i] >= 0) {
        continue;
      }
      if(rg[i].empty()) {
        return {};
      }
      es.emplace_back(rg[i][0], i);
    }
    return es;
  }

  // left: [0,n), right: [n,n+m), S: n+m, T: n+m+1
  vector< vector< int > > build_risidual_graph() {
    if(!matched) max_matching();
    const size_t S = n + m;
    const size_t T = n + m + 1;
    vector< vector< int > > ris(n + m + 2);
    for(int i = 0; i < n; i++) {
      if(match_l[i] == -1) ris[S].emplace_back(i);
      else ris[i].emplace_back(S);
    }
    for(int i = 0; i < m; i++) {
      if(match_r[i] == -1) ris[i + n].emplace_back(T);
      else ris[T].emplace_back(i + n);
    }
    for(int i = 0; i < n; i++) {
      for(auto &j : g[i]) {
        if(match_l[i] == j) ris[j + n].emplace_back(i);
        else ris[i].emplace_back(j + n);
      }
    }
    return ris;
  }

private:
  vector< int > find_residual_path() {
    auto res = build_risidual_graph();
    queue< int > que;
    vector< int > visited(n + m + 2);
    que.emplace(n + m);
    visited[n + m] = true;
    while(!que.empty()) {
      int idx = que.front();
      que.pop();
      for(auto &to : res[idx]) {
        if(visited[to]) continue;
        visited[to] = true;
        que.emplace(to);
      }
    }
    return visited;
  }

  void build_augment_path() {
    queue< int > que;
    dist.assign(g.size(), -1);
    for(int i = 0; i < n; i++) {
      if(match_l[i] == -1) {
        que.emplace(i);
        dist[i] = 0;
      }
    }
    while(!que.empty()) {
      int a = que.front();
      que.pop();
      for(auto &b : g[a]) {
        int c = match_r[b];
        if(c >= 0 && dist[c] == -1) {
          dist[c] = dist[a] + 1;
          que.emplace(c);
        }
      }
    }
  }

  bool find_min_dist_augment_path(int a) {
    used[a] = time_stamp;
    for(auto &b : g[a]) {
      int c = match_r[b];
      if(c < 0 || (used[c] != time_stamp && dist[c] == dist[a] + 1 && find_min_dist_augment_path(c))) {
        match_r[b] = a;
        match_l[a] = b;
        return true;
      }
    }
    return false;
  }

  bool find_augment_path(int a) {
    used[a] = time_stamp;
    for(auto &b : g[a]) {
      int c = match_r[b];
      if(c < 0 || (alive[c] == 1 && used[c] != time_stamp && find_augment_path(c))) {
        match_r[b] = a;
        match_l[a] = b;
        return true;
      }
    }
    return false;
  }
};
#line 6 "test/verify/yosupo-bipartitematching.test.cpp"

int main() {
  int L, R, M;
  cin >> L >> R >> M;
  BipartiteFlow flow(L, R);
  for(int i = 0; i < M; i++) {
    int a, b;
    cin >> a >> b;
    flow.add_edge(a, b);
  }
  auto es = flow.max_matching();
  cout << es.size() << "\n";
  for(auto &p : es) cout << p.first << " " << p.second << "\n";
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

