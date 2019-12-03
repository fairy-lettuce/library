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


# :warning: math/number-theory/quotient-range.cpp
* category: math/number-theory


[Back to top page](../../../index.html)



## Code
```cpp
template< typename T >
vector< pair< pair< T, T >, T > > quotient_range(T N) {
  T M;
  vector< pair< pair< T, T >, T > > ret;
  for(M = 1; M * M <= N; M++) {
    ret.emplace_back(make_pair(M, M), N / M);
  }
  for(T i = M; i >= 1; i--) {
    T L = N / (i + 1) + 1;
    T R = N / i;
    if(L <= R && ret.back().first.second < L) ret.emplace_back(make_pair(L, R), N / L);
  }
  return ret;
}

```

[Back to top page](../../../index.html)

