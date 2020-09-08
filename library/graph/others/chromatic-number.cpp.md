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
<script type="text/javascript" src="../../../assets/js/copy-button.js"></script>
<link rel="stylesheet" href="../../../assets/css/copy-button.css" />


# :heavy_check_mark: Chromatic-Number(彩色数) <small>(graph/others/chromatic-number.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#e557c7f962c39680942b9dada22cabec">graph/others</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/others/chromatic-number.cpp">View this file on GitHub</a>
    - Last commit date: 2020-09-08 23:29:00+09:00


* see: <a href="https://www.slideshare.net/wata_orz/ss-12131479">https://www.slideshare.net/wata_orz/ss-12131479</a>


## 概要

グラフの彩色数を求める. 彩色数とは, 隣接する頂点が異なる色となるように彩色するために必要な最小色数である.

あるグラフが $k$ 彩色可能であることと, $k$ 個の独立集合で被覆できることは必要十分条件である. つまり独立集合から $k$ 個の頂点を選んで被覆する方法の総数が求まれば良い. これはbit DPと包除原理を用いて効率的に求められる.

## 使い方

* `chromatic_number(g)`: 隣接行列 `g` で表されるグラフの彩色数を求める.

## 計算量

* $O(2^N N)$


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-1254.test.cpp.html">test/verify/aoj-1254.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Chromatic-Number(彩色数)
 * @docs docs/chromatic-number.md
 * @see https://www.slideshare.net/wata_orz/ss-12131479
 */
template< typename Matrix >
int chromatic_number(Matrix &g) {
  int N = (int) g.size();
  vector< int > es(N);
  for(int i = 0; i < g.size(); i++) {
    for(int j = 0; j < g.size(); j++) {
      if(g[i][j] != 0) es[i] |= 1 << j;
    }
  }
  int ret = N;
  for(int d : {7, 11, 21}) {
    int mod = 1e9 + d;
    vector< int > ind(1 << N), aux(1 << N, 1);
    ind[0] = 1;
    for(int S = 1; S < 1 << N; S++) {
      int u = __builtin_ctz(S);
      ind[S] = ind[S ^ (1 << u)] + ind[(S ^ (1 << u)) & ~es[u]];
    }
    for(int i = 1; i < ret; i++) {
      int64_t all = 0;
      for(int j = 0; j < 1 << N; j++) {
        int S = j ^(j >> 1);
        aux[S] = (1LL * aux[S] * ind[S]) % mod;
        all += j & 1 ? aux[S] : mod - aux[S];
      }
      if(all % mod) ret = i;
    }
  }
  return ret;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "graph/others/chromatic-number.cpp"
/**
 * @brief Chromatic-Number(彩色数)
 * @docs docs/chromatic-number.md
 * @see https://www.slideshare.net/wata_orz/ss-12131479
 */
template< typename Matrix >
int chromatic_number(Matrix &g) {
  int N = (int) g.size();
  vector< int > es(N);
  for(int i = 0; i < g.size(); i++) {
    for(int j = 0; j < g.size(); j++) {
      if(g[i][j] != 0) es[i] |= 1 << j;
    }
  }
  int ret = N;
  for(int d : {7, 11, 21}) {
    int mod = 1e9 + d;
    vector< int > ind(1 << N), aux(1 << N, 1);
    ind[0] = 1;
    for(int S = 1; S < 1 << N; S++) {
      int u = __builtin_ctz(S);
      ind[S] = ind[S ^ (1 << u)] + ind[(S ^ (1 << u)) & ~es[u]];
    }
    for(int i = 1; i < ret; i++) {
      int64_t all = 0;
      for(int j = 0; j < 1 << N; j++) {
        int S = j ^(j >> 1);
        aux[S] = (1LL * aux[S] * ind[S]) % mod;
        all += j & 1 ? aux[S] : mod - aux[S];
      }
      if(all % mod) ret = i;
    }
  }
  return ret;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

