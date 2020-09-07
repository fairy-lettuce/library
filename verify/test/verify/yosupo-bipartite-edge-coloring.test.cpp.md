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


# :heavy_check_mark: test/verify/yosupo-bipartite-edge-coloring.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yosupo-bipartite-edge-coloring.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-26 02:20:26+09:00


* see: <a href="https://judge.yosupo.jp/problem/bipartite_edge_coloring">https://judge.yosupo.jp/problem/bipartite_edge_coloring</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/graph/flow/bipartite-flow.cpp.html">Bipartite-Flow(二部グラフのフロー) <small>(graph/flow/bipartite-flow.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/graph/others/bipartite-graph-edge-coloring.cpp.html">Bipartite-Graph-Edge-Coloring(二部グラフの辺彩色) <small>(graph/others/bipartite-graph-edge-coloring.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/graph/others/eulerian-trail.cpp.html">Eulerian-Trail(オイラー路) <small>(graph/others/eulerian-trail.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/structure/union-find/union-find.cpp.html">Union-Find <small>(structure/union-find/union-find.cpp)</small></a>
* :question: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://judge.yosupo.jp/problem/bipartite_edge_coloring"

#include "../../template/template.cpp"

#include "../../structure/union-find/union-find.cpp"

#include "../../graph/flow/bipartite-flow.cpp"
#include "../../graph/others/eulerian-trail.cpp"
#include "../../graph/others/bipartite-graph-edge-coloring.cpp"

int main() {
  int L, R, M;
  cin >> L >> R >> M;
  BipariteGraphEdgeColoring ecbg;
  for(int i = 0; i < M; i++) {
    int a, b;
    cin >> a >> b;
    ecbg.add_edge(a, b);
  }
  auto res = ecbg.build();
  cout << res.size() << "\n";
  vector< int > color(M);
  for(int i = 0; i < res.size(); i++) {
    for(auto &j : res[i]) color[j] = i;
  }
  for(auto &c : color) cout << c << "\n";
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yosupo-bipartite-edge-coloring.test.cpp"
#define PROBLEM "https://judge.yosupo.jp/problem/bipartite_edge_coloring"

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
#line 4 "test/verify/yosupo-bipartite-edge-coloring.test.cpp"

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
#line 6 "test/verify/yosupo-bipartite-edge-coloring.test.cpp"

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
#line 1 "graph/others/eulerian-trail.cpp"
/**
 * @brief Eulerian-Trail(オイラー路)
 */
template< bool directed >
struct EulerianTrail {
  vector< vector< pair< int, int > > > g;
  vector< pair< int, int > > es;
  int M;
  vector< int > used_vertex, used_edge, deg;

  explicit EulerianTrail(int V) : g(V), M(0), deg(V), used_vertex(V) {}

  void add_edge(int a, int b) {
    es.emplace_back(a, b);
    g[a].emplace_back(b, M);
    if(directed) {
      deg[a]++;
      deg[b]--;
    } else {
      g[b].emplace_back(a, M);
      deg[a]++;
      deg[b]++;
    }
    M++;
  }

  pair< int, int > get_edge(int idx) const {
    return es[idx];
  }

  vector< vector< int > > enumerate_eulerian_trail() {
    if(directed) {
      for(auto &p : deg) if(p != 0) return {};
    } else {
      for(auto &p : deg) if(p & 1) return {};
    }
    used_edge.assign(M, 0);
    vector< vector< int > > ret;
    for(int i = 0; i < (int) g.size(); i++) {
      if(g[i].empty() || used_vertex[i]) continue;
      ret.emplace_back(go(i));
    }
    return ret;
  }

  vector< vector< int > > enumerate_semi_eulerian_trail() {
    UnionFind uf(g.size());
    for(auto &p : es) uf.unite(p.first, p.second);
    vector< vector< int > > group(g.size());
    for(int i = 0; i < (int) g.size(); i++) group[uf.find(i)].emplace_back(i);
    vector< vector< int > > ret;
    used_edge.assign(M, 0);
    for(auto &vs : group) {
      if(vs.empty()) continue;
      int latte = -1, malta = -1;
      if(directed) {
        for(auto &p : vs) {
          if(abs(deg[p]) > 1) {
            return {};
          } else if(deg[p] == 1) {
            if(latte >= 0) return {};
            latte = p;
          }
        }
      } else {
        for(auto &p : vs) {
          if(deg[p] & 1) {
            if(latte == -1) latte = p;
            else if(malta == -1) malta = p;
            else return {};
          }
        }
      }
      ret.emplace_back(go(latte == -1 ? vs.front() : latte));
      if(ret.back().empty()) ret.pop_back();
    }
    return ret;
  }

  vector< int > go(int s) {
    stack< pair< int, int > > st;
    vector< int > ord;
    st.emplace(s, -1);
    while(!st.empty()) {
      int idx = st.top().first;
      used_vertex[idx] = true;
      if(g[idx].empty()) {
        ord.emplace_back(st.top().second);
        st.pop();
      } else {
        auto e = g[idx].back();
        g[idx].pop_back();
        if(used_edge[e.second]) continue;
        used_edge[e.second] = true;
        st.emplace(e);
      }
    }
    ord.pop_back();
    reverse(ord.begin(), ord.end());
    return ord;
  }
};
#line 1 "graph/others/bipartite-graph-edge-coloring.cpp"
/**
 * @brief Bipartite-Graph-Edge-Coloring(二部グラフの辺彩色)
 * @see https://ei1333.hateblo.jp/entry/2020/08/25/015955
 */
struct BipariteGraphEdgeColoring {
private:
  vector< vector< int > > ans;
  vector< int > A, B;
  int L, R;

  struct RegularGraph {
    int k{}, n{};
    vector< int > A, B;
  };
  RegularGraph g;

  static UnionFind contract(valarray< int > &deg, int k) {
    using pi = pair< int, int >;
    priority_queue< pi, vector< pi >, greater<> > que;
    for(int i = 0; i < (int) deg.size(); i++) {
      que.emplace(deg[i], i);
    }
    UnionFind uf(deg.size());
    while(que.size() > 1) {
      auto p = que.top();
      que.pop();
      auto q = que.top();
      que.pop();
      if(p.first + q.first > k) continue;
      p.first += q.first;
      uf.unite(p.second, q.second);
      que.emplace(p);
    }
    return uf;
  }


  RegularGraph build_k_regular_graph() {
    valarray< int > deg[2];
    deg[0] = valarray< int >(L);
    deg[1] = valarray< int >(R);
    for(auto &p : A) deg[0][p]++;
    for(auto &p : B) deg[1][p]++;

    int k = max(deg[0].max(), deg[1].max());

    /* step 1 */
    UnionFind uf[2];
    uf[0] = contract(deg[0], k);
    uf[1] = contract(deg[1], k);

    vector< int > id[2];
    int ptr[] = {0, 0};
    id[0] = vector< int >(L);
    id[1] = vector< int >(R);
    for(int i = 0; i < L; i++) if(uf[0].find(i) == i) id[0][i] = ptr[0]++;
    for(int i = 0; i < R; i++) if(uf[1].find(i) == i) id[1][i] = ptr[1]++;

    /* step 2 */
    int N = max(ptr[0], ptr[1]);
    deg[0] = valarray< int >(N);
    deg[1] = valarray< int >(N);

    /* step 3 */
    vector< int > C, D;
    C.reserve(N * k);
    D.reserve(N * k);
    for(int i = 0; i < (int) A.size(); i++) {
      int u = id[0][uf[0].find(A[i])];
      int v = id[1][uf[1].find(B[i])];
      C.emplace_back(u);
      D.emplace_back(v);
      deg[0][u]++;
      deg[1][v]++;
    }
    int j = 0;
    for(int i = 0; i < N; i++) {
      while(deg[0][i] < k) {
        while(deg[1][j] == k) ++j;
        C.emplace_back(i);
        D.emplace_back(j);
        ++deg[0][i];
        ++deg[1][j];
      }
    }

    return {k, N, C, D};
  }

  void rec(const vector< int > &ord, int k) {
    if(k == 0) {
      return;
    } else if(k == 1) {
      ans.emplace_back(ord);
      return;
    } else if((k & 1) == 0) {
      EulerianTrail< false > et(g.n + g.n);
      for(auto &p : ord) et.add_edge(g.A[p], g.B[p] + g.n);
      auto paths = et.enumerate_eulerian_trail();
      vector< int > path;
      for(auto &ps : paths) {
        for(auto &e : ps) path.emplace_back(ord[e]);
      }
      vector< int > beet[2];
      for(int i = 0; i < (int) path.size(); i++) {
        beet[i & 1].emplace_back(path[i]);
      }
      rec(beet[0], k / 2);
      rec(beet[1], k / 2);
    } else {
      BipartiteFlow flow(g.n, g.n);
      for(auto &i : ord) flow.add_edge(g.A[i], g.B[i]);
      flow.max_matching();
      vector< int > beet;
      ans.emplace_back();
      for(auto &i : ord) {
        if(flow.match_l[g.A[i]] == g.B[i]) {
          flow.match_l[g.A[i]] = -1;
          ans.back().emplace_back(i);
        } else {
          beet.emplace_back(i);
        }
      }
      rec(beet, k - 1);
    }
  }

public:
  explicit BipariteGraphEdgeColoring() : L(0), R(0) {}

  void add_edge(int a, int b) {
    A.emplace_back(a);
    B.emplace_back(b);
    L = max(L, a + 1);
    R = max(R, b + 1);
  }

  vector< vector< int > > build() {
    g = build_k_regular_graph();
    vector< int > ord(g.A.size());
    iota(ord.begin(), ord.end(), 0);
    rec(ord, g.k);
    vector< vector< int > > res;
    for(int i = 0; i < (int) ans.size(); i++) {
      res.emplace_back();
      for(auto &j : ans[i]) if(j < A.size()) res.back().emplace_back(j);
    }
    return res;
  }
};
#line 10 "test/verify/yosupo-bipartite-edge-coloring.test.cpp"

int main() {
  int L, R, M;
  cin >> L >> R >> M;
  BipariteGraphEdgeColoring ecbg;
  for(int i = 0; i < M; i++) {
    int a, b;
    cin >> a >> b;
    ecbg.add_edge(a, b);
  }
  auto res = ecbg.build();
  cout << res.size() << "\n";
  vector< int > color(M);
  for(int i = 0; i < res.size(); i++) {
    for(auto &j : res[i]) color[j] = i;
  }
  for(auto &c : color) cout << c << "\n";
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

