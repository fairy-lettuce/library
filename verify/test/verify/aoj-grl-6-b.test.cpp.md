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


# :warning: test/verify/aoj-grl-6-b.test.cpp


[Back to top page](../../../index.html)

* see: [http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_6_B](http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_6_B)


## Dependencies
* :warning: [graph/flow/primal-dual.cpp](../../../library/graph/flow/primal-dual.cpp.html)
* :warning: [graph/template.cpp](../../../library/graph/template.cpp.html)
* :warning: [template/template.cpp](../../../library/template/template.cpp.html)


## Code
```cpp
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_6_B"

#include "../../template/template.cpp"
#include "../../graph/template.cpp"

#include "../../graph/flow/primal-dual.cpp"


int main() {
  int V, E, F;
  scanf("%d %d %d", &V, &E, &F);
  PrimalDual< int, int > g(V);
  for(int i = 0; i < E; i++) {
    int a, b, c, d;
    scanf("%d %d %d %d", &a, &b, &c, &d);
    g.add_edge(a, b, c, d);
  }
  printf("%d\n", g.min_cost_flow(0, V - 1, F));
}

```

[Back to top page](../../../index.html)

