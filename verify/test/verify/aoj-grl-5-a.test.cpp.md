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


# :warning: test/verify/aoj-grl-5-a.test.cpp


[Back to top page](../../../index.html)

* see: [http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_5_A](http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_5_A)


## Dependencies
* :warning: [graph/template.cpp](../../../library/graph/template.cpp.html)
* :warning: [graph/tree/tree-diameter.cpp](../../../library/graph/tree/tree-diameter.cpp.html)
* :warning: [template/template.cpp](../../../library/template/template.cpp.html)


## Code
```cpp
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_5_A"

#include "../../template/template.cpp"
#include "../../graph/template.cpp"

#include "../../graph/tree/tree-diameter.cpp"

int main() {
  int N;
  scanf("%d", &N);
  WeightedGraph< int > g(N);
  for(int i = 1; i < N; i++) {
    int x, y, z;
    scanf("%d %d %d", &x, &y, &z);
    g[x].emplace_back(y, z);
    g[y].emplace_back(x, z);
  }
  printf("%d\n", tree_diameter(g));
}

```

[Back to top page](../../../index.html)

