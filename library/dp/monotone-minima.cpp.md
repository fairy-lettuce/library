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


# :heavy_check_mark: Monotone-Minima <small>(dp/monotone-minima.cpp)</small>

<a href="../../index.html">Back to top page</a>

* category: <a href="../../index.html#95687afb5d9a2a9fa39038f991640b0c">dp</a>
* <a href="{{ site.github.repository_url }}/blob/master/dp/monotone-minima.cpp">View this file on GitHub</a>
    - Last commit date: 2020-02-24 21:29:56+09:00




## 概要

$2$ 変数関数 $f(i, j) (0 \leq i \lt H, 0 \leq j \lt W)$ が Monotone であるとは, すべての $k$ に対して $\mathrm{argmin} f(k, *) \leq \mathrm{argmin} f(k + 1, *)$ を満たすことをいう. つまり各行の最小値をとる位置が右下に単調に下がっていることを意味する.

Monge $\Rightarrow$ Totally Monotone(TM) $\Rightarrow$ Monotone なので, Monotone は弱い条件である.

* `monotone_minima(H, W, f, comp)`: 各行について, 最小値をとる位置と最小値をペアで返す. `f` は $2$ 変数関数, `comp` は比較関数.

## 計算量

* $O(N \log N)$


## Verified with

* :heavy_check_mark: <a href="../../verify/test/verify/aoj-2603.test.cpp.html">test/verify/aoj-2603.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/test/verify/yukicoder-703.test.cpp.html">test/verify/yukicoder-703.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/test/verify/yukicoder-704.test.cpp.html">test/verify/yukicoder-704.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/test/verify/yukicoder-705.test.cpp.html">test/verify/yukicoder-705.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
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

```
{% endraw %}

<a href="../../index.html">Back to top page</a>

