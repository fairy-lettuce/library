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


# :warning: graph/shortest-path/dijkstra-fibonacchi-heap.cpp
* category: graph/shortest-path


[Back to top page](../../../index.html)



## Verified
* :warning: [test/verify/aoj-grl-1-a-2.test.cpp](../../../verify/test/verify/aoj-grl-1-a-2.test.cpp.html)


## Code
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

[Back to top page](../../../index.html)

