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


# :warning: tree/verify/aoj-grl-5-c.test.cpp


[Back to top page](../../../index.html)

* see: [http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_5_C](http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_5_C)


## Dependencies
* :warning: [graph/template.cpp](../../../library/graph/template.cpp.html)
* :warning: [template/template.cpp](../../../library/template/template.cpp.html)
* :warning: [tree/doubling-lowest-common-ancestor.cpp](../../../library/tree/doubling-lowest-common-ancestor.cpp.html)


## Code
```cpp
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_5_C"

#include "../../template/template.cpp"
#include "../../graph/template.cpp"

#include "../doubling-lowest-common-ancestor.cpp"

int main() {
  int N, Q;
  scanf("%d", &N);
  UnWeightedGraph g(N);
  for(int i = 0; i < N; i++) {
    int k;
    scanf("%d", &k);
    while(k--) {
      int c;
      scanf("%d", &c);
      g[i].push_back(c);
    }
  }
  DoublingLowestCommonAncestor< UnWeightedGraph > lca(g);
  lca.build();
  scanf("%d", &Q);
  while(Q--) {
    int x, y;
    scanf("%d %d", &x, &y);
    printf("%d\n", lca.query(x, y));
  }
}

```

[Back to top page](../../../index.html)

