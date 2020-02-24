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


# :heavy_check_mark: math/fft/number-theoretic-transform-friendly-mod-int.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#f2e6b7734e19ae7657e83160bba9f2e7">math/fft</a>
* <a href="{{ site.github.repository_url }}/blob/master/math/fft/number-theoretic-transform-friendly-mod-int.cpp">View this file on GitHub</a>
    - Last commit date: 2020-02-24 19:19:55+09:00




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-bellnoulli-number.test.cpp.html">test/verify/yosupo-bellnoulli-number.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-exp-of-formal-power-series.test.cpp.html">test/verify/yosupo-exp-of-formal-power-series.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-inv-of-formal-power-series.test.cpp.html">test/verify/yosupo-inv-of-formal-power-series.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-log-of-formal-power-series.test.cpp.html">test/verify/yosupo-log-of-formal-power-series.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-multipoint-evaluation.test.cpp.html">test/verify/yosupo-multipoint-evaluation.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-partition-function.test.cpp.html">test/verify/yosupo-partition-function.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-polynomial-interpolation.test.cpp.html">test/verify/yosupo-polynomial-interpolation.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-sqrt-of-formal-power-series.test.cpp.html">test/verify/yosupo-sqrt-of-formal-power-series.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
template< typename Mint >
struct NumberTheoreticTransformFriendlyModInt {

  vector< Mint > dw, idw;
  int max_base;
  Mint root;

  NumberTheoreticTransformFriendlyModInt() {
    const unsigned mod = Mint::get_mod();
    assert(mod >= 3 && mod % 2 == 1);
    auto tmp = mod - 1;
    max_base = 0;
    while(tmp % 2 == 0) tmp >>= 1, max_base++;
    root = 2;
    while(root.pow((mod - 1) >> 1) == 1) root += 1;
    assert(root.pow(mod - 1) == 1);
    dw.resize(max_base);
    idw.resize(max_base);
    for(int i = 0; i < max_base; i++) {
      dw[i] = -root.pow((mod - 1) >> (i + 2));
      idw[i] = Mint(1) / dw[i];
    }
  }

  void ntt(vector< Mint > &a) {
    const int n = (int) a.size();
    assert((n & (n - 1)) == 0);
    assert(__builtin_ctz(n) <= max_base);
    for(int m = n; m >>= 1;) {
      Mint w = 1;
      for(int s = 0, k = 0; s < n; s += 2 * m) {
        for(int i = s, j = s + m; i < s + m; ++i, ++j) {
          auto x = a[i], y = a[j] * w;
          a[i] = x + y, a[j] = x - y;
        }
        w *= dw[__builtin_ctz(++k)];
      }
    }
  }

  void intt(vector< Mint > &a, bool f = true) {
    const int n = (int) a.size();
    assert((n & (n - 1)) == 0);
    assert(__builtin_ctz(n) <= max_base);
    for(int m = 1; m < n; m *= 2) {
      Mint w = 1;
      for(int s = 0, k = 0; s < n; s += 2 * m) {
        for(int i = s, j = s + m; i < s + m; ++i, ++j) {
          auto x = a[i], y = a[j];
          a[i] = x + y, a[j] = (x - y) * w;
        }
        w *= idw[__builtin_ctz(++k)];
      }
    }
    if(f) {
      Mint inv_sz = Mint(1) / n;
      for(int i = 0; i < n; i++) a[i] *= inv_sz;
    }
  }

  vector< Mint > multiply(vector< Mint > a, vector< Mint > b) {
    int need = a.size() + b.size() - 1;
    int nbase = 1;
    while((1 << nbase) < need) nbase++;
    int sz = 1 << nbase;
    a.resize(sz, 0);
    b.resize(sz, 0);
    ntt(a);
    ntt(b);
    Mint inv_sz = Mint(1) / sz;
    for(int i = 0; i < sz; i++) a[i] *= b[i] * inv_sz;
    intt(a, false);
    a.resize(need);
    return a;
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "math/fft/number-theoretic-transform-friendly-mod-int.cpp"
template< typename Mint >
struct NumberTheoreticTransformFriendlyModInt {

  vector< Mint > dw, idw;
  int max_base;
  Mint root;

  NumberTheoreticTransformFriendlyModInt() {
    const unsigned mod = Mint::get_mod();
    assert(mod >= 3 && mod % 2 == 1);
    auto tmp = mod - 1;
    max_base = 0;
    while(tmp % 2 == 0) tmp >>= 1, max_base++;
    root = 2;
    while(root.pow((mod - 1) >> 1) == 1) root += 1;
    assert(root.pow(mod - 1) == 1);
    dw.resize(max_base);
    idw.resize(max_base);
    for(int i = 0; i < max_base; i++) {
      dw[i] = -root.pow((mod - 1) >> (i + 2));
      idw[i] = Mint(1) / dw[i];
    }
  }

  void ntt(vector< Mint > &a) {
    const int n = (int) a.size();
    assert((n & (n - 1)) == 0);
    assert(__builtin_ctz(n) <= max_base);
    for(int m = n; m >>= 1;) {
      Mint w = 1;
      for(int s = 0, k = 0; s < n; s += 2 * m) {
        for(int i = s, j = s + m; i < s + m; ++i, ++j) {
          auto x = a[i], y = a[j] * w;
          a[i] = x + y, a[j] = x - y;
        }
        w *= dw[__builtin_ctz(++k)];
      }
    }
  }

  void intt(vector< Mint > &a, bool f = true) {
    const int n = (int) a.size();
    assert((n & (n - 1)) == 0);
    assert(__builtin_ctz(n) <= max_base);
    for(int m = 1; m < n; m *= 2) {
      Mint w = 1;
      for(int s = 0, k = 0; s < n; s += 2 * m) {
        for(int i = s, j = s + m; i < s + m; ++i, ++j) {
          auto x = a[i], y = a[j];
          a[i] = x + y, a[j] = (x - y) * w;
        }
        w *= idw[__builtin_ctz(++k)];
      }
    }
    if(f) {
      Mint inv_sz = Mint(1) / n;
      for(int i = 0; i < n; i++) a[i] *= inv_sz;
    }
  }

  vector< Mint > multiply(vector< Mint > a, vector< Mint > b) {
    int need = a.size() + b.size() - 1;
    int nbase = 1;
    while((1 << nbase) < need) nbase++;
    int sz = 1 << nbase;
    a.resize(sz, 0);
    b.resize(sz, 0);
    ntt(a);
    ntt(b);
    Mint inv_sz = Mint(1) / sz;
    for(int i = 0; i < sz; i++) a[i] *= b[i] * inv_sz;
    intt(a, false);
    a.resize(need);
    return a;
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

