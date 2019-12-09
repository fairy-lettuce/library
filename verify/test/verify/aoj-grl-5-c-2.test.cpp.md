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


# :heavy_check_mark: test/verify/aoj-grl-5-c-2.test.cpp


[Back to top page](../../../index.html)

* see: [http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_5_C](http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_5_C)


## Dependencies
* :heavy_check_mark: [graph/template.cpp](../../../library/graph/template.cpp.html)
* :heavy_check_mark: [graph/tree/heavy-light-decomposition.cpp](../../../library/graph/tree/heavy-light-decomposition.cpp.html)
* :heavy_check_mark: [template/template.cpp](../../../library/template/template.cpp.html)


## Code
{% raw %}
```cpp
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_5_C"

#include "../../template/template.cpp"
#include "../../graph/template.cpp"

#include "../../graph/tree/heavy-light-decomposition.cpp"

int main() {
  int N, Q;
  scanf("%d", &N);
  UnWeightedGraph g(N);
  HeavyLightDecomposition< UnWeightedGraph > tree(g);
  for(int i = 0; i < N; i++) {
    int k;
    scanf("%d", &k);
    for(int j = 0; j < k; j++) {
      int c;
      scanf("%d", &c);
      g[i].push_back(c);
    }
  }
  tree.build();
  scanf("%d", &Q);
  for(int i = 0; i < Q; i++) {
    int u, v;
    scanf("%d %d", &u, &v);
    printf("%d\n", tree.lca(u, v));
  }
}

```
{% endraw %}

[Back to top page](../../../index.html)

