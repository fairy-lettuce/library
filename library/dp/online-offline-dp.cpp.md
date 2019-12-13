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


# :warning: dp/online-offline-dp.cpp
<a href="../../index.html">Back to top page</a>

* category: <a href="../../index.html#95687afb5d9a2a9fa39038f991640b0c">dp</a>
* <a href="{{ site.github.repository_url }}/blob/master/dp/online-offline-dp.cpp">View this file on GitHub</a>
    - Last commit date: 2019-07-20 01:29:30 +0900




## Code
{% raw %}
```cpp
template< typename T, typename Compare = less< T > >
vector< T > online_offline_dp(int W, const function< T(int, int) > &f, const Compare &comp = Compare()) {
  vector< T > dp(W + 1);
  vector< int > isset(W + 1);
  int y_base = -1, x_base = -1;
  function< T(int, int) > get_cost = [&](int y, int x) { // return dp[0, x+x_base)+f[x+x_base, y+y_base)
    return dp[x + x_base] + f(x + x_base, y + y_base);
  };
  function< void(int, int, int) > induce = [&](int l, int m, int r) { // dp[l, m) -> dp[m, r)
    x_base = l, y_base = m;
    auto ret = monotone_minima(r - m, m - l, get_cost, comp);
    for(int i = 0; i < ret.size(); i++) {
      if(!isset[m + i] || comp(ret[i].second, dp[m + i])) {
        isset[m + i] = true;
        dp[m + i] = ret[i].second;
      }
    }
  };
  function< void(int, int) > dfs = [&](int l, int r) {
    if(l + 1 == r) {
      x_base = l, y_base = l;
      T cst = l ? get_cost(0, -1) : 0;
      if(!isset[l] || comp(cst, dp[l])) {
        isset[l] = true;
        dp[l] = cst;
      }
    } else {
      int mid = (l + r) / 2;
      dfs(l, mid);
      induce(l, mid, r);
      dfs(mid, r);
    }
  };
  dfs(0, W + 1);
  return dp;
};

```
{% endraw %}

<a href="../../index.html">Back to top page</a>

