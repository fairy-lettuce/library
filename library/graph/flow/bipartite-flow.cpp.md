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


# :heavy_check_mark: Bipartite-Flow(二部グラフのフロー) <small>(graph/flow/bipartite-flow.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#2af6c4bb6ad7cfa010303133dc15971f">graph/flow</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/flow/bipartite-flow.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-10 19:29:34+09:00




## 概要

二部グラフに対するフロー. 

最大マッチングは Hopcroft-Karp に基づく実装. 最大流を求める Dinic と同じアルゴリズムだが, Hopcroft-Karp はこれを二部グラフ用に書き換えたもので定数倍が軽い. 残余グラフをBFSして各頂点までの最短距離を計算し, 最短距離のパスをDFSで見つけてフローを流す.

計算量が良いため基本的にはこれを使うと良い.

## 残余グラフについて
左側の頂点を $[0, n)$, 右側の頂点を $[n, n+m)$, 始点を $n+m$, 終点を $n+m+1$ としたグラフの残余グラフを用いると, いろいろできる.

このグラフを強連結成分分解する. すると各辺 $(u, v)$ (実際には $(u, v+n)$ なので注意すること) について, その辺が最大マッチングに必ず使うか, 必ず使わないか, それ以外かが分かり, 以下の手順で確認できる.

1. 頂点 $u, v$ が同じ強連結成分に含まれる → それ以外
2. 辺 $(u, v)$ が最大マッチングに含まれる → 必ず使う
3. それ以外(頂点 $u, v$ が異なる連結成分) → 必ず使わない

残余グラフについて始点から到達できる頂点をBFSなどにより全列挙する. 最小頂点被覆は, 左側かつ到達できない頂点 または 右側かつ到達できる点である. 最大安定集合はその補集合である. また残余グラフを見て頑張ると同じ計算量で辞書順最小頂点被覆も求まる.

## DAG の最小パス被覆

グラフ $G = (V, E)$ において, そのグラフの全ての頂点が $1$ つ以上のパスに含まれるようなパスの集合をを パス被覆 という.

特に, パス被覆の中でパスの数が最小のものを 最小パス被覆 という.

DAGの最小パス被覆は二部グラフの最大マッチング問題に帰着できる. 頂点を倍長して, 始点を左側に, 終点を右側に配置したグラフを考える. $V$ 本のパスがあれば被覆できることは自明. このグラフのマッチング一組に対して必要なパスを $1$ つ減らすことができるため, $V - $ (二部グラフの最大マッチング) が最小パス被覆となる.

## 使い方

* `BipartiteFlow(n, m)`:= 左側の頂点数 `n`, 右側の頂点数 `m` で初期化する.
* `add_edge(u, v)`:= 頂点 `u`, `v` 間に辺を張る.
* `max_matching()`:= 最大マッチングを返す.
* `min_vertex_cover()`:= 最小頂点被覆を返す.
* `max_independent_set()`:= 最大安定集合を返す.
* `min_edge_cover()`:= 最小辺被覆を返す.
* `lex_max_matching()`:= 辞書順最小の最大マッチングを返す.
* `lex_min_vertex_cover(ord)`:= `ord` は左側の頂点を $[0, n)$, 右側の頂点を $[n, n + m)$ で表すとき, 優先度が高い順に頂点番号を並べた長さ $n + m$ の数列. このときの辞書順(優先度順)最小頂点被覆を返す.
* `build_residual_graph()`:= 左側の頂点を $[0, n)$, 右側の頂点を $[n, n+m)$, 始点を $n+m$, 終点を $n+m+1$ としたグラフを考えたとき, 残余グラフを返す.

## 計算量

* `max_matching()`: $O(E \sqrt V)$
* `min_vertex_cover()`: $O(E \sqrt V)$
* `max_vertex_cover()`: $O(E \sqrt V)$
* `min_edge_cover()`: $O(E \sqrt V)$
* `lex_max_matching()`: $O(E V)$ だと思うが早くできるのかも
* `lex_min_vertex_cover(ord)`: $O(E \sqrt V)$
* `build_residual_graph()`: $O(E + V)$



## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-0334.test.cpp.html">test/verify/aoj-0334.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-bipartitematching.test.cpp.html">test/verify/yosupo-bipartitematching.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
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

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
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

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

