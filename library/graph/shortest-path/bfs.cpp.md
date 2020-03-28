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


# :heavy_check_mark: BFS(幅優先探索) <small>(graph/shortest-path/bfs.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#73feb47c464a017d041247d88424b879">graph/shortest-path</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/shortest-path/bfs.cpp">View this file on GitHub</a>
    - Last commit date: 2020-03-28 23:32:32+09:00




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-alds-1-11-c.test.cpp.html">test/verify/aoj-alds-1-11-c.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
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

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
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

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

