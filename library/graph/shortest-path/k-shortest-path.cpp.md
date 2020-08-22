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


# :heavy_check_mark: K-Shortest-Path <small>(graph/shortest-path/k-shortest-path.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#73feb47c464a017d041247d88424b879">graph/shortest-path</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/shortest-path/k-shortest-path.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-22 20:09:30+09:00


* see: <a href="https://qiita.com/nariaki3551/items/821dc6ffdc552d3d5f22">https://qiita.com/nariaki3551/items/821dc6ffdc552d3d5f22</a>


## 概要

頂点 $s$ から $t$ へのパス(Path) のうち, 昇順 $k$ 個のパスの長さを Yen's Algorithm により求める. 

パス(Path, 道) は同じ頂点を通らない経路である.

verify が甘いため合っているかかなり不安です

* `k_shotest_path(g, s, t, k)`: 重み付き有向グラフ `g` の頂点 `s` から `t` へのウォークのうち, 昇順 `k` 個のパスの長さとそのパスの辺番号の列を返す(パスの個数が `k` 個に満たないとき全てを返す).

## 計算量

* $O(KV ((E + v) \log V))$


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/yukicoder-1069.test.cpp.html">test/verify/yukicoder-1069.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
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

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
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

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

