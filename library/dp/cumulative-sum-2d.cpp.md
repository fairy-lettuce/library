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


# :heavy_check_mark: Cumulative-Sum-2D(二次元累積和) <small>(dp/cumulative-sum-2d.cpp)</small>

<a href="../../index.html">Back to top page</a>

* category: <a href="../../index.html#95687afb5d9a2a9fa39038f991640b0c">dp</a>
* <a href="{{ site.github.repository_url }}/blob/master/dp/cumulative-sum-2d.cpp">View this file on GitHub</a>
    - Last commit date: 2020-05-15 00:48:56+09:00




## 概要

$2$ 次元の累積和. 前計算として事前に累積和をとることで, 矩形和を $O(1)$ で求めることが出来る.

* `add(x, y, z)`: 要素 $(x, y)$ に値 `z` を加える.
* `build()`: 累積和を構築する.
* `query(sx, sy, gx, gy)`: 左下 $(sx, sy)$, 右上 $(gx, gy)$ の矩形和を求める(半開区間で与えることに注意すること. 具体的には列 $gx$ と行 $gy$ は含まない).

## 計算量

* `add(k, x, y)`: $O(1)$
* `build()`: $O(WH)$
* `query(sx, sy, gx, gy)`: $O(1)$


## Verified with

* :heavy_check_mark: <a href="../../verify/test/verify/aoj-0560.test.cpp.html">test/verify/aoj-0560.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Cumulative-Sum-2D(二次元累積和)
 * @docs docs/cumulative-sum-2d.md
*/
template< class T >
struct CumulativeSum2D {
  vector< vector< T > > data;

  CumulativeSum2D(int W, int H) : data(W + 1, vector< int >(H + 1, 0)) {}

  void add(int x, int y, T z) {
    ++x, ++y;
    if(x >= data.size() || y >= data[0].size()) return;
    data[x][y] += z;
  }

  void build() {
    for(int i = 1; i < data.size(); i++) {
      for(int j = 1; j < data[i].size(); j++) {
        data[i][j] += data[i][j - 1] + data[i - 1][j] - data[i - 1][j - 1];
      }
    }
  }

  T query(int sx, int sy, int gx, int gy) const {
    return (data[gx][gy] - data[sx][gy] - data[gx][sy] + data[sx][sy]);
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "dp/cumulative-sum-2d.cpp"
/**
 * @brief Cumulative-Sum-2D(二次元累積和)
 * @docs docs/cumulative-sum-2d.md
*/
template< class T >
struct CumulativeSum2D {
  vector< vector< T > > data;

  CumulativeSum2D(int W, int H) : data(W + 1, vector< int >(H + 1, 0)) {}

  void add(int x, int y, T z) {
    ++x, ++y;
    if(x >= data.size() || y >= data[0].size()) return;
    data[x][y] += z;
  }

  void build() {
    for(int i = 1; i < data.size(); i++) {
      for(int j = 1; j < data[i].size(); j++) {
        data[i][j] += data[i][j - 1] + data[i - 1][j] - data[i - 1][j - 1];
      }
    }
  }

  T query(int sx, int sy, int gx, int gy) const {
    return (data[gx][gy] - data[sx][gy] - data[gx][sy] + data[sx][sy]);
  }
};

```
{% endraw %}

<a href="../../index.html">Back to top page</a>

