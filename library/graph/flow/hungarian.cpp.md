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


# :warning: graph/flow/hungarian.cpp
* category: graph/flow


[Back to top page](../../../index.html)



## Code
```cpp
template< typename T >
T hungarian(Matrix< T > &A) {
  const T infty = numeric_limits< T >::max();
  const int N = (int) A.size();
  const int M = (int) A[0].size();
  vector< int > P(M), way(M);
  vector< T > U(N, 0), V(M, 0), minV;
  vector< bool > used;

  for(int i = 1; i < N; i++) {
    P[0] = i;
    minV.assign(M, infty);
    used.assign(M, false);
    int j0 = 0;
    while(P[j0] != 0) {
      int i0 = P[j0], j1 = 0;
      used[j0] = true;
      T delta = infty;
      for(int j = 1; j < M; j++) {
        if(used[j]) continue;
        T curr = A[i0][j] - U[i0] - V[j];
        if(curr < minV[j]) minV[j] = curr, way[j] = j0;
        if(minV[j] < delta) delta = minV[j], j1 = j;
      }
      for(int j = 0; j < M; j++) {
        if(used[j]) U[P[j]] += delta, V[j] -= delta;
        else minV[j] -= delta;
      }
      j0 = j1;
    }
    do {
      P[j0] = P[way[j0]];
      j0 = way[j0];
    } while(j0 != 0);
  }
  return -V[0];
}

```

[Back to top page](../../../index.html)

