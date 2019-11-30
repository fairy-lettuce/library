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
<script type="text/javascript" src="../../assets/js/copy-button.js"></script>
<link rel="stylesheet" href="../../assets/css/copy-button.css" />


# :warning: graph/prim-fibonacchi-heap.cpp
* category: graph


[Back to top page](../../index.html)



## Verified
* :warning: [graph/verify/aoj-grl-2-a-4.test.cpp](../../verify/graph/verify/aoj-grl-2-a-4.test.cpp.html)


## Code
```cpp
template< typename T >
T prim_fibonacchi_heap(WeightedGraph< T > &g) {
  const auto INF = numeric_limits< T >::max();
  using Heap = FibonacchiHeap< T, int >;
  using Node = typename Heap::Node;
  using Pi = pair< T, int >;

  T total = 0;
  vector< T > dist(g.size(), INF);
  vector< int > used(g.size());
  Heap heap;
  vector< Node * > keep(g.size(), nullptr);
  dist[0] = 0;
  keep[0] = heap.push(0, 0);

  while(!heap.empty()) {
    T cost;
    int idx;
    tie(cost, idx) = heap.pop();
    if(used[idx]) continue;
    used[idx] = true;
    total += cost;
    for(auto &e : g[idx]) {
      if(used[e.to] || dist[e.to] <= e.cost) continue;
      if(keep[e.to] == nullptr) {
        dist[e.to] = e.cost;
        keep[e.to] = heap.push(e.cost, e.to);
      } else {
        T d = dist[e.to] - e.cost;
        heap.decrease_key(keep[e.to], d);
        dist[e.to] -= d;
      }
    }
  }
  return total;
}

```

[Back to top page](../../index.html)

