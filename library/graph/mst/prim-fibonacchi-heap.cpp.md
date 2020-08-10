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


# :heavy_check_mark: Prim-Fibonacchi-Heap(最小全域木) <small>(graph/mst/prim-fibonacchi-heap.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#51f95ed2fd9ed3be34f576d38fbd25a2">graph/mst</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/mst/prim-fibonacchi-heap.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-10 20:09:21+09:00




## 概要

最小全域木(全域木のうち, その辺群の重みの総和が最小になる木)を求める.

通常の prim 法では `std::priority_queue` を使用していたが, これをフィボナッチヒープにすることで計算量を落とせる(実用上早くなるかは知らない).

* `prim_fibonacchi_heap(g)`: 連結な重み付きグラフ `g` の最小全域木を求める. `cost` には辺の重みの総和, `edges` にはそれを構成する辺が格納される.

## 計算量

* $O(V \log V + E)$ 


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-grl-2-a-4.test.cpp.html">test/verify/aoj-grl-2-a-4.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Prim-Fibonacchi-Heap(最小全域木)
 * @docs docs/prim-fibonacchi-heap.md
 */
template< typename T >
struct MinimumSpanningTree {
  T cost;
  Edges< T > edges;
};

template< typename T >
MinimumSpanningTree< T > prim_fibonacchi_heap(Graph< T > &g) {
  const auto INF = numeric_limits< T >::max();
  using Heap = FibonacchiHeap< T, int >;
  using Node = typename Heap::Node;
  using Pi = pair< T, int >;

  T total = 0;
  vector< Edge< T > * > dist(g.size());
  vector< int > used(g.size());
  Heap heap;
  vector< Node * > keep(g.size(), nullptr);
  keep[0] = heap.push(0, 0);
  Edges< T > es;
  while(!heap.empty()) {
    T cost;
    int idx;
    tie(cost, idx) = heap.pop();
    if(used[idx]) continue;
    used[idx] = true;
    total += cost;
    if(dist[idx]) es.emplace_back(*dist[idx]);
    for(auto &e : g.g[idx]) {
      if(used[e.to] || (dist[e.to] && dist[e.to]->cost <= e.cost)) continue;
      if(keep[e.to] == nullptr) {
        dist[e.to] = &e;
        keep[e.to] = heap.push(e.cost, e.to);
      } else {
        T d = dist[e.to]->cost - e.cost;
        heap.decrease_key(keep[e.to], d);
        dist[e.to] = &e;
      }
    }
  }
  return {total, es};
}


```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "graph/mst/prim-fibonacchi-heap.cpp"
/**
 * @brief Prim-Fibonacchi-Heap(最小全域木)
 * @docs docs/prim-fibonacchi-heap.md
 */
template< typename T >
struct MinimumSpanningTree {
  T cost;
  Edges< T > edges;
};

template< typename T >
MinimumSpanningTree< T > prim_fibonacchi_heap(Graph< T > &g) {
  const auto INF = numeric_limits< T >::max();
  using Heap = FibonacchiHeap< T, int >;
  using Node = typename Heap::Node;
  using Pi = pair< T, int >;

  T total = 0;
  vector< Edge< T > * > dist(g.size());
  vector< int > used(g.size());
  Heap heap;
  vector< Node * > keep(g.size(), nullptr);
  keep[0] = heap.push(0, 0);
  Edges< T > es;
  while(!heap.empty()) {
    T cost;
    int idx;
    tie(cost, idx) = heap.pop();
    if(used[idx]) continue;
    used[idx] = true;
    total += cost;
    if(dist[idx]) es.emplace_back(*dist[idx]);
    for(auto &e : g.g[idx]) {
      if(used[e.to] || (dist[e.to] && dist[e.to]->cost <= e.cost)) continue;
      if(keep[e.to] == nullptr) {
        dist[e.to] = &e;
        keep[e.to] = heap.push(e.cost, e.to);
      } else {
        T d = dist[e.to]->cost - e.cost;
        heap.decrease_key(keep[e.to], d);
        dist[e.to] = &e;
      }
    }
  }
  return {total, es};
}


```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

