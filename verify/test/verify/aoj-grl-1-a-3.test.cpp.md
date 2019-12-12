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


# :warning: test/verify/aoj-grl-1-a-3.test.cpp
<a href="../../../index.html">Back to top page</a>

* <a href="{{ site.github.repository_url }}/blob/master/test/verify/aoj-grl-1-a-3.test.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 23:02:43 +0900


* see: <a href="http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_1_A">http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_1_A</a>


## Depends On
* :warning: <a href="../../../library/graph/shortest-path/dijkstra-radix-heap.cpp.html">graph/shortest-path/dijkstra-radix-heap.cpp</a>
* :warning: <a href="../../../library/graph/template.cpp.html">graph/template.cpp</a>
* :warning: <a href="../../../library/structure/heap/radix-heap.cpp.html">structure/heap/radix-heap.cpp</a>
* :warning: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code
{% raw %}
```cpp
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_1_A"

#include "../../template/template.cpp"
#include "../../graph/template.cpp"

#include "../../structure/heap/radix-heap.cpp"

#include "../../graph/shortest-path/dijkstra-radix-heap.cpp"

int main() {
  int V, E, R;
  scanf("%d %d %d", &V, &E, &R);
  WeightedGraph< int > g(V);
  for(int i = 0; i < E; i++) {
    int a, b, c;
    scanf("%d %d %d", &a, &b, &c);
    g[a].emplace_back(b, c);
  }
  for(auto &dist : dijkstra_radix_heap(g, R)) {
    if(dist == numeric_limits< int >::max()) puts("INF");
    else printf("%d\n", dist);
  }
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

