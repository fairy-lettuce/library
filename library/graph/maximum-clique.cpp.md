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
<script type="text/javascript" src="../../assets/js/copy-button.js"></script>
<link rel="stylesheet" href="../../assets/css/copy-button.css" />


# :warning: graph/maximum-clique.cpp
* category: graph


[Back to top page](../../index.html)



## Code
```cpp
template< typename T >
T maximum_clique(Matrix< bool > g, function< T(vector< int >) > f) {

  int N = (int) g.size(), M = 0;
  vector< int > deg(N), v(N);
  for(int i = 0; i < N; i++) {
    for(int j = 0; j < i; j++) {
      assert(g[i][j] == g[j][i]);
      if(g[i][j]) {
        ++deg[i];
        ++M;
      }
    }
  }
  T t = 0;
  int lim = (int) sqrt(2 * M);

  for(int i = 0; i < N; i++) {
    vector< int > notice;
    for(int j = 0; j < N; j++) {
      if(!v[j] && deg[j] < lim) {
        for(int k = 0; k < N; k++) {
          if(j == k) continue;
          if(g[j][k]) notice.emplace_back(k);
        }
        notice.emplace_back(j);
        break;
      }
    }
    if(notice.empty()) break;
    int neighbor = (int) notice.size() - 1;
    vector< int > bit(neighbor);
    for(int j = 0; j < neighbor; j++) {
      for(int k = 0; k < j; k++) {
        if(!g[notice[j]][notice[k]]) {
          bit[j] |= 1 << k;
          bit[k] |= 1 << j;
        }
      }
    }
    for(int j = 0; j < (1 << neighbor); j++) {
      bool ok = true;
      for(int k = 0; k < neighbor; k++) {
        if((j >> k) & 1) ok &= (j & bit[k]) == 0;
      }
      if(ok) {
        vector< int > stock{notice.back()};
        for(int k = 0; k < neighbor; k++) {
          if((j >> k) & 1) stock.emplace_back(notice[k]);
        }
        t = max(t, f(stock));
      }
    }
    v[notice.back()] = true;
    for(int j = 0; j < N; j++) {
      if(g[j][notice.back()]) {
        --deg[j];
        g[notice.back()][j] = g[j][notice.back()] = false;
      }
    }
  }

  vector< int > notice;
  for(int j = 0; j < N; j++) {
    if(!v[j]) notice.emplace_back(j);
  }
  int neighbor = (int) notice.size();
  vector< int > bit(neighbor);
  for(int j = 0; j < neighbor; j++) {
    for(int k = 0; k < j; k++) {
      if(!g[notice[j]][notice[k]]) {
        bit[j] |= 1 << k;
        bit[k] |= 1 << j;
      }
    }
  }
  for(int j = 0; j < (1 << neighbor); j++) {
    bool ok = true;
    for(int k = 0; k < neighbor; k++) {
      if((j >> k) & 1) ok &= (j & bit[k]) == 0;
    }
    if(ok) {
      vector< int > stock;
      for(int k = 0; k < neighbor; k++) {
        if((j >> k) & 1) stock.emplace_back(notice[k]);
      }
      t = max(t, f(stock));
    }
  }
  return t;
}


```

[Back to top page](../../index.html)

