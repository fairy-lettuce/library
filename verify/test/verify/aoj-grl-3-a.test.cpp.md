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


# :heavy_check_mark: test/verify/aoj-grl-3-a.test.cpp


[Back to top page](../../../index.html)

* see: [http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_3_A](http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_3_A)


## Dependencies
* :heavy_check_mark: [graph/others/lowlink.cpp](../../../library/graph/others/lowlink.cpp.html)
* :heavy_check_mark: [graph/template.cpp](../../../library/graph/template.cpp.html)
* :heavy_check_mark: [template/template.cpp](../../../library/template/template.cpp.html)


## Code
```cpp
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_3_A"

#include "../../template/template.cpp"
#include "../../graph/template.cpp"

#include "../../graph/others/lowlink.cpp"

int main() {
  int V, E;
  scanf("%d %d", &V, &E);
  UnWeightedGraph g(V);
  for(int i = 0; i < E; i++) {
    int x, y;
    scanf("%d %d", &x, &y);
    g[x].push_back(y);
    g[y].push_back(x);
  }
  LowLink< UnWeightedGraph > lowlink(g);
  lowlink.build();
  sort(lowlink.articulation.begin(), lowlink.articulation.end());
  for(auto &v : lowlink.articulation) printf("%d\n", v);
}

```

[Back to top page](../../../index.html)

