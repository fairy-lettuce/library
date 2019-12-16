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


# :heavy_check_mark: graph/shortest-path/dijkstra-fibonacchi-heap.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#73feb47c464a017d041247d88424b879">graph/shortest-path</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/shortest-path/dijkstra-fibonacchi-heap.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 23:02:43 +0900




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-grl-1-a-2.test.cpp.html">test/verify/aoj-grl-1-a-2.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
template< typename T >
vector< T > dijkstra_fibonacchi_heap(WeightedGraph< T > &g, int s) {
  const auto INF = numeric_limits< T >::max();
  using Heap = FibonacchiHeap< T, int >;
  using Node = typename Heap::Node;
  using Pi = pair< T, int >;

  Heap heap;
  vector< Node * > keep(g.size(), nullptr);
  vector< T > dist;
  dist.assign(g.size(), INF);
  dist[s] = 0;
  keep[s] = heap.push(dist[s], s);

  while(!heap.empty()) {
    T cost;
    int idx;
    tie(cost, idx) = heap.pop();
    if(dist[idx] < cost) continue;
    for(auto &e : g[idx]) {
      auto next_cost = cost + e.cost;
      if(dist[e.to] <= next_cost) continue;
      if(keep[e.to] == nullptr) {
        dist[e.to] = next_cost;
        keep[e.to] = heap.push(dist[e.to], e.to);
      } else {
        T d = dist[e.to] - next_cost;
        heap.decrease_key(keep[e.to], d);
        dist[e.to] -= d;
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
#line 1 "graph/shortest-path/dijkstra-fibonacchi-heap.cpp"
template< typename T >
vector< T > dijkstra_fibonacchi_heap(WeightedGraph< T > &g, int s) {
  const auto INF = numeric_limits< T >::max();
  using Heap = FibonacchiHeap< T, int >;
  using Node = typename Heap::Node;
  using Pi = pair< T, int >;

  Heap heap;
  vector< Node * > keep(g.size(), nullptr);
  vector< T > dist;
  dist.assign(g.size(), INF);
  dist[s] = 0;
  keep[s] = heap.push(dist[s], s);

  while(!heap.empty()) {
    T cost;
    int idx;
    tie(cost, idx) = heap.pop();
    if(dist[idx] < cost) continue;
    for(auto &e : g[idx]) {
      auto next_cost = cost + e.cost;
      if(dist[e.to] <= next_cost) continue;
      if(keep[e.to] == nullptr) {
        dist[e.to] = next_cost;
        keep[e.to] = heap.push(dist[e.to], e.to);
      } else {
        T d = dist[e.to] - next_cost;
        heap.decrease_key(keep[e.to], d);
        dist[e.to] -= d;
      }
    }
  }
  return dist;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

