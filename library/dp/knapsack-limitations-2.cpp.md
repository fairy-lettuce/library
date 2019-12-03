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


# :warning: dp/knapsack-limitations-2.cpp
* category: dp


[Back to top page](../../index.html)



## Verified
* :warning: [test/verify/aoj-dpl-1-i.test.cpp](../../verify/test/verify/aoj-dpl-1-i.test.cpp.html)


## Code
```cpp
template< typename T >
T knapsack_limitations(const vector< T > &w, const vector< T > &m, const vector< int > &v,
                       const T &W) {
  const int N = (int) w.size();
  auto v_max = *max_element(begin(v), end(v));
  if(v_max == 0) return 0;
  vector< int > ma(N);
  vector< T > mb(N);
  for(int i = 0; i < N; i++) {
    ma[i] = min< T >(m[i], v_max - 1);
    mb[i] = m[i] - ma[i];
  }
  T sum = 0;
  for(int i = 0; i < N; i++) sum += ma[i] * v[i];
  auto dp = knapsack_limitations(v, ma, w, sum, T(-1), less<>());
  vector< int > ord(N);
  iota(begin(ord), end(ord), 0);
  sort(begin(ord), end(ord), [&](int a, int b) {
    return v[a] * w[b] > v[b] * w[a];
  });
  T ret = T();
  for(int i = 0; i < dp.size(); i++) {
    if(dp[i] > W || dp[i] == -1) continue;
    T rest = W - dp[i], cost = i;
    for(auto &p : ord) {
      auto get = min(mb[p], rest / w[p]);
      if(get == 0) break;
      cost += get * v[p];
      rest -= get * w[p];
    }
    ret = max(ret, cost);
  }
  return ret;
}

```

[Back to top page](../../index.html)

