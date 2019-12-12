---
layout: default
---

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


# :warning: dp/divide-and-conquer-optimization.cpp
<a href="../../index.html">Back to top page</a>

* category: dp
* <a href="{{ site.github.repository_url }}/blob/master/dp/divide-and-conquer-optimization.cpp">View this file on GitHub</a>
    - Last commit date: 2019-07-20 01:29:30 +0900




## Code
{% raw %}
```cpp
template< typename T, typename Compare = less< T > >
vector< vector< T > > divide_and_conquer_optimization(int H, int W, T INF, const function< T(int, int) > &f, const Compare &comp = Compare()) {
  vector< vector< T > > dp(H + 1, vector< T >(W + 1, INF));
  dp[0][0] = 0;
  for(int i = 1; i <= H; i++) {
    function< T(int, int) > get_cost = [&](int y, int x) {
      if(x >= y) return INF;
      return dp[i - 1][x] + f(x, y);
    };
    auto ret = monotone_minima(W + 1, W + 1, get_cost, comp);
    for(int j = 0; j <= W; j++) dp[i][j] = ret[j].second;
  }
  return dp;
}

```
{% endraw %}

<a href="../../index.html">Back to top page</a>

