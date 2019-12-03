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


# :warning: test/verify/aoj-grl-1-c.test.cpp


[Back to top page](../../../index.html)

* see: [http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_1_C](http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_1_C)


## Dependencies
* :warning: [graph/shortest-path/warshall-floyd.cpp](../../../library/graph/shortest-path/warshall-floyd.cpp.html)
* :warning: [graph/template.cpp](../../../library/graph/template.cpp.html)
* :warning: [template/template.cpp](../../../library/template/template.cpp.html)


## Code
```cpp
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_1_C"

#include "../../template/template.cpp"
#include "../../graph/template.cpp"

#include "../../graph/shortest-path/warshall-floyd.cpp"

int main() {
  int V, E;
  scanf("%d %d", &V, &E);
  Matrix< int > mat(V, vector< int >(V, INT_MAX));
  for(int i = 0; i < V; i++) mat[i][i] = 0;
  for(int i = 0; i < E; i++) {
    int x, y, z;
    scanf("%d %d %d", &x, &y, &z);
    mat[x][y] = z;
  }
  warshall_floyd(mat, INT_MAX);
  for(int i = 0; i < V; i++) {
    if(mat[i][i] < 0) {
      puts("NEGATIVE CYCLE");
      return 0;
    }
  }
  for(int i = 0; i < V; i++) {
    for(int j = 0; j < V; j++) {
      if(j > 0) putchar(' ');
      if(mat[i][j] == INT_MAX) printf("INF");
      else printf("%d", mat[i][j]);
    }
    putchar('\n');
  }
}

```

[Back to top page](../../../index.html)

