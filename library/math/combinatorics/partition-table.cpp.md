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


# :warning: math/combinatorics/partition-table.cpp
* category: math/combinatorics


[Back to top page](../../../index.html)



## Verified
* :heavy_check_mark: [test/verify/aoj-dpl-5-j.test.cpp](../../../verify/test/verify/aoj-dpl-5-j.test.cpp.html)


## Code
```cpp
template< typename T >
vector< vector< T > > get_partition(int n, int k) {
  vector< vector< T > > dp(n + 1, vector< T >(k + 1));
  dp[0][0] = 1;
  for(int i = 0; i <= n; i++) {
    for(int j = 1; j <= k; j++) {
      if(i - j >= 0) dp[i][j] = dp[i][j - 1] + dp[i - j][j];
      else dp[i][j] = dp[i][j - 1];
    }
  }
  return dp;
}

```

[Back to top page](../../../index.html)

