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


# :warning: Cumulative-Sum(一次元累積和) <small>(dp/cumulative-sum.cpp)</small>

<a href="../../index.html">Back to top page</a>

* category: <a href="../../index.html#95687afb5d9a2a9fa39038f991640b0c">dp</a>
* <a href="{{ site.github.repository_url }}/blob/master/dp/cumulative-sum.cpp">View this file on GitHub</a>
    - Last commit date: 2020-02-20 22:23:04+09:00




## 概要

$1$ 次元の累積和. 前計算として事前に累積和をとることで, 区間の和を $O(1)$ で求めることが出来る.

* `add(k, x)`: 要素 `k` に値 `x` を加える.
* `build()`: 累積和を構築する.
* `query(k)`: 区間 $[0, k]$ の和を求める(閉区間なので注意).


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Cumulative-Sum(一次元累積和)
 * @docs docs/cumulative-sum.md
 */
template< class T >
struct CumulativeSum {
  vector< T > data;

  CumulativeSum() = default;

  explicit CumulativeSum(size_t sz) : data(sz, 0) {}

  void add(int k, const T &x) {
    data[k] += x;
  }

  void build() {
    for(int i = 1; i < data.size(); i++) {
      data[i] += data[i - 1];
    }
  }

  T query(int k) const {
    if(k < 0) return 0;
    return data[min(k, (int) data.size() - 1)];
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "dp/cumulative-sum.cpp"
/**
 * @brief Cumulative-Sum(一次元累積和)
 * @docs docs/cumulative-sum.md
 */
template< class T >
struct CumulativeSum {
  vector< T > data;

  CumulativeSum() = default;

  explicit CumulativeSum(size_t sz) : data(sz, 0) {}

  void add(int k, const T &x) {
    data[k] += x;
  }

  void build() {
    for(int i = 1; i < data.size(); i++) {
      data[i] += data[i - 1];
    }
  }

  T query(int k) const {
    if(k < 0) return 0;
    return data[min(k, (int) data.size() - 1)];
  }
};

```
{% endraw %}

<a href="../../index.html">Back to top page</a>

