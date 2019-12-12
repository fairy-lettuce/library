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


# :warning: graph/mst/chu-liu-edmond.cpp
<a href="../../../index.html">Back to top page</a>

* category: graph/mst
* <a href="{{ site.github.repository_url }}/blob/master/graph/mst/chu-liu-edmond.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 23:02:43 +0900




## Verified With
* :warning: <a href="../../../verify/test/verify/aoj-grl-2-b.test.cpp.html">test/verify/aoj-grl-2-b.test.cpp</a>


## Code
{% raw %}
```cpp
template< typename T >
struct MinimumSpanningTreeArborescence
{
  using Pi = pair< T, int >;
  using Heap = SkewHeap< Pi, int >;
  using Node = typename Heap::Node;
  const Edges< T > &es;
  const int V;
  T INF;
 
  MinimumSpanningTreeArborescence(const Edges< T > &es, int V) :
      INF(numeric_limits< T >::max()), es(es), V(V) {}
 
  T build(int start)
  {
    auto g = [](const Pi &a, const T &b) { return Pi(a.first + b, a.second); };
    auto h = [](const T &a, const T &b) { return a + b; };
    Heap heap(g, h);
    vector< Node * > heaps(V, heap.makeheap());
    for(auto &e : es) heap.push(heaps[e.to], {e.cost, e.src});
    UnionFind uf(V);
    vector< int > used(V, -1);
    used[start] = start;
 
    T ret = 0;
    for(int s = 0; s < V; s++) {
      stack< int > path;
      for(int u = s; used[u] < 0;) {
        path.push(u);
        used[u] = s;
        if(heap.empty(heaps[u])) return -1;
        auto p = heap.top(heaps[u]);
        ret += p.first;
        heap.add(heaps[u], -p.first);
        heap.pop(heaps[u]);
        int v = uf.find(p.second);
        if(used[v] == s) {
          int w;
          Node *nextheap = heap.makeheap();
          do {
            w = path.top();
            path.pop();
            nextheap = heap.merge(nextheap, heaps[w]);
          } while(uf.unite(v, w));
          heaps[uf.find(v)] = nextheap;
          used[uf.find(v)] = -1;
        }
        u = uf.find(v);
      }
    }
    return ret;
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

