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


# :heavy_check_mark: test/verify/aoj-grl-2-b.test.cpp


[Back to top page](../../../index.html)

* see: [http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_2_B](http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_2_B)


## Dependencies
* :heavy_check_mark: [graph/mst/chu-liu-edmond.cpp](../../../library/graph/mst/chu-liu-edmond.cpp.html)
* :heavy_check_mark: [graph/template.cpp](../../../library/graph/template.cpp.html)
* :heavy_check_mark: [structure/heap/skew-heap.cpp](../../../library/structure/heap/skew-heap.cpp.html)
* :heavy_check_mark: [structure/union-find/union-find.cpp](../../../library/structure/union-find/union-find.cpp.html)
* :heavy_check_mark: [template/template.cpp](../../../library/template/template.cpp.html)


## Code
{% raw %}
```cpp
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_2_B"

#include "../../template/template.cpp"
#include "../../graph/template.cpp"

#include "../../structure/union-find/union-find.cpp"
#include "../../structure/heap/skew-heap.cpp"

#include "../../graph/mst/chu-liu-edmond.cpp"

int main() {
  int V, E, R;
  scanf("%d %d %d", &V, &E, &R);
  Edges< int > edges;
  for(int i = 0; i < E; i++) {
    int a, b, c;
    scanf("%d %d %d", &a, &b, &c);
    edges.emplace_back(a, b, c);
  }
  printf("%d\n", MinimumSpanningTreeArborescence< int >(edges, V).build(R));
}

```
{% endraw %}

[Back to top page](../../../index.html)

