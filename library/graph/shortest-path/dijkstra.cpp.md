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


# :question: Dijkstra(単一始点最短路) <small>(graph/shortest-path/dijkstra.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#73feb47c464a017d041247d88424b879">graph/shortest-path</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/shortest-path/dijkstra.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-21 01:30:35+09:00




## 概要

負辺のないグラフで単一始点全点間最短路を求めるアルゴリズム. 各地点でもっとも近い頂点から距離が確定していく. 距離順でソートされたヒープを用いると, 効率よく距離を確定していくことができる.

* `dijkstra(g, s)`: 重み付きグラフ `g` で, 頂点 `s` から全点間の最短コストを求める. `dist` には最短コスト(到達できないとき型の最大値), `from` にはその頂点の直前に訪れた頂点(頂点 `s` または到達できない頂点は $-1$), `id` はその頂点の直前に使った辺番号が格納される.

## 計算量

* $O(E \log V)$ 


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-0275.test.cpp.html">test/verify/aoj-0275.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-grl-1-a.test.cpp.html">test/verify/aoj-grl-1-a.test.cpp</a>
* :x: <a href="../../../verify/test/verify/yosupo-k-shortest-walk.test.cpp.html">test/verify/yosupo-k-shortest-walk.test.cpp</a>
* :x: <a href="../../../verify/test/verify/yosupo-shortest-path.test.cpp.html">test/verify/yosupo-shortest-path.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
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

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
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

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

