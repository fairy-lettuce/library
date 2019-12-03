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


# :warning: math/combinatorics/lagrange-polynomial.cpp
* category: math/combinatorics


[Back to top page](../../../index.html)



## Code
```cpp
template< typename T >
T lagrange_polynomial(const vector< T > &y, int64_t t) {
  int N = y.size() - 1;
  Combination< T > comb(N);
  if(t <= N) return y[t];
  T ret(0);
  vector< T > dp(N + 1, 1), pd(N + 1, 1);
  for(int i = 0; i < N; i++) dp[i + 1] = dp[i] * (t - i);
  for(int i = N; i > 0; i--) pd[i - 1] = pd[i] * (t - i);
  for(int i = 0; i <= N; i++) {
    T tmp = y[i] * dp[i] * pd[i] * comb.rfact(i) * comb.rfact(N - i);
    if((N - i) & 1) ret -= tmp;
    else ret += tmp;
  }
  return ret;
}

```

[Back to top page](../../../index.html)

