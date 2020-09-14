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


# :heavy_check_mark: Online-Offline-DP(オンライン・オフライン変換) <small>(dp/online-offline-dp.cpp)</small>

<a href="../../index.html">Back to top page</a>

* category: <a href="../../index.html#95687afb5d9a2a9fa39038f991640b0c">dp</a>
* <a href="{{ site.github.repository_url }}/blob/master/dp/online-offline-dp.cpp">View this file on GitHub</a>
    - Last commit date: 2020-09-15 00:43:54+09:00




## 概要

$dp[j] = \min \\{ dp[i] + f(i,j) : i \in [0,j) \\}$ (例: $f(i,j)$ を区間 $[i,j)$ のコストとすると、区間[0, j) を任意個に分割するときの最小コスト) を考える.

愚直にDPをすると $O(N^2)$ かかるが, 最小値をとる位置 $i$ が $j$ の増加にしたがって単調増加する場合 $O(N \log^2 N)$ で解くことができる.

区間 $[l, r)$ の dp 配列を埋めたい. $m = \frac {l + r} 2$ とする.
遷移するときに $m$ をまたがないものは分割して再帰的に解くことにすると, $m$ をまたぐものだけを考えれば良い. $[l, m)$ の dp 配列の値はわかり, それ以前の dp の計算結果に依存しない形となる. つまり $2$ 変数関数 $g(j, i) = dp[i] + f(i, j) (l \le i \lt m, m \leq j \lt r)$ を定義できて, Monotone-Minima を用いて効率的に解くことができる. (日本語むずかしい　こまった）(分割統治FFTも同じ考え方なので下のコードのinduceの部分をFFTにするとできると思う)


* `online_offline_dp(N, f, comp)`: 長さ $N + 1$ の dp 配列($dp[j]:=$ 区間 $[0, j)$ を任意個に分割するときのコスト) を返す. $f(i, j)$ は区間 $[i, j)$ のコストを与える $2$ 変数関数($0 \leq i \lt j \leq N$ を満たす範囲で定義されていればよい).

## 計算量

* $O(N \log^2 N)$


## Depends on

* :heavy_check_mark: <a href="monotone-minima.cpp.html">Monotone-Minima <small>(dp/monotone-minima.cpp)</small></a>


## Verified with

* :heavy_check_mark: <a href="../../verify/test/verify/yukicoder-703.test.cpp.html">test/verify/yukicoder-703.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/test/verify/yukicoder-704.test.cpp.html">test/verify/yukicoder-704.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/test/verify/yukicoder-705.test.cpp.html">test/verify/yukicoder-705.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#include "monotone-minima.cpp"

/**
 * @brief  Online-Offline-DP(オンライン・オフライン変換)
 * @docs docs/online-offline-dp.md
 */
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

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "dp/monotone-minima.cpp"
/**
 * @brief Monotone-Minima
 * @docs docs/monotone-minima.md
 */
template< typename T, typename Compare = less< T > >
vector< pair< int, T > > monotone_minima(int H, int W, const function< T(int, int) > &f, const Compare &comp = Compare()) {
  vector< pair< int, T > > dp(H);
  function< void(int, int, int, int) > dfs = [&](int top, int bottom, int left, int right) {
    if(top > bottom) return;
    int line = (top + bottom) / 2;
    T ma;
    int mi = -1;
    for(int i = left; i <= right; i++) {
      T cst = f(line, i);
      if(mi == -1 || comp(cst, ma)) {
        ma = cst;
        mi = i;
      }
    }
    dp[line] = make_pair(mi, ma);
    dfs(top, line - 1, left, mi);
    dfs(line + 1, bottom, mi, right);
  };
  dfs(0, H - 1, 0, W - 1);
  return dp;
}
#line 2 "dp/online-offline-dp.cpp"

/**
 * @brief  Online-Offline-DP(オンライン・オフライン変換)
 * @docs docs/online-offline-dp.md
 */
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

