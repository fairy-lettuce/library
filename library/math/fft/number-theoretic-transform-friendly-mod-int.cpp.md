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
    - Last commit date: 2019-12-03 22:21:44 +0900




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

  vector< int > rev;
  vector< Mint > rts;
  int base, max_base;
  Mint root;

  NumberTheoreticTransformFriendlyModInt() : base(1), rev{0, 1}, rts{0, 1} {
    const int mod = Mint::get_mod();
    assert(mod >= 3 && mod % 2 == 1);
    auto tmp = mod - 1;
    max_base = 0;
    while(tmp % 2 == 0) tmp >>= 1, max_base++;
    root = 2;
    while(root.pow((mod - 1) >> 1) == 1) root += 1;
    assert(root.pow(mod - 1) == 1);
    root = root.pow((mod - 1) >> max_base);
  }

  void ensure_base(int nbase) {
    if(nbase <= base) return;
    rev.resize(1 << nbase);
    rts.resize(1 << nbase);
    for(int i = 0; i < (1 << nbase); i++) {
      rev[i] = (rev[i >> 1] >> 1) + ((i & 1) << (nbase - 1));
    }
    assert(nbase <= max_base);
    while(base < nbase) {
      Mint z = root.pow(1 << (max_base - 1 - base));
      for(int i = 1 << (base - 1); i < (1 << base); i++) {
        rts[i << 1] = rts[i];
        rts[(i << 1) + 1] = rts[i] * z;
      }
      ++base;
    }
  }


  void ntt(vector< Mint > &a) {
    const int n = (int) a.size();
    assert((n & (n - 1)) == 0);
    int zeros = __builtin_ctz(n);
    ensure_base(zeros);
    int shift = base - zeros;
    for(int i = 0; i < n; i++) {
      if(i < (rev[i] >> shift)) {
        swap(a[i], a[rev[i] >> shift]);
      }
    }
    for(int k = 1; k < n; k <<= 1) {
      for(int i = 0; i < n; i += 2 * k) {
        for(int j = 0; j < k; j++) {
          Mint z = a[i + j + k] * rts[j + k];
          a[i + j + k] = a[i + j] - z;
          a[i + j] = a[i + j] + z;
        }
      }
    }
  }


  void intt(vector< Mint > &a) {
    const int n = (int) a.size();
    ntt(a);
    reverse(a.begin() + 1, a.end());
    Mint inv_sz = Mint(1) / n;
    for(int i = 0; i < n; i++) a[i] *= inv_sz;
  }

  vector< Mint > multiply(vector< Mint > a, vector< Mint > b) {
    int need = a.size() + b.size() - 1;
    int nbase = 1;
    while((1 << nbase) < need) nbase++;
    ensure_base(nbase);
    int sz = 1 << nbase;
    a.resize(sz, 0);
    b.resize(sz, 0);
    ntt(a);
    ntt(b);
    Mint inv_sz = Mint(1) / sz;
    for(int i = 0; i < sz; i++) {
      a[i] *= b[i] * inv_sz;
    }
    reverse(a.begin() + 1, a.end());
    ntt(a);
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

  vector< int > rev;
  vector< Mint > rts;
  int base, max_base;
  Mint root;

  NumberTheoreticTransformFriendlyModInt() : base(1), rev{0, 1}, rts{0, 1} {
    const int mod = Mint::get_mod();
    assert(mod >= 3 && mod % 2 == 1);
    auto tmp = mod - 1;
    max_base = 0;
    while(tmp % 2 == 0) tmp >>= 1, max_base++;
    root = 2;
    while(root.pow((mod - 1) >> 1) == 1) root += 1;
    assert(root.pow(mod - 1) == 1);
    root = root.pow((mod - 1) >> max_base);
  }

  void ensure_base(int nbase) {
    if(nbase <= base) return;
    rev.resize(1 << nbase);
    rts.resize(1 << nbase);
    for(int i = 0; i < (1 << nbase); i++) {
      rev[i] = (rev[i >> 1] >> 1) + ((i & 1) << (nbase - 1));
    }
    assert(nbase <= max_base);
    while(base < nbase) {
      Mint z = root.pow(1 << (max_base - 1 - base));
      for(int i = 1 << (base - 1); i < (1 << base); i++) {
        rts[i << 1] = rts[i];
        rts[(i << 1) + 1] = rts[i] * z;
      }
      ++base;
    }
  }


  void ntt(vector< Mint > &a) {
    const int n = (int) a.size();
    assert((n & (n - 1)) == 0);
    int zeros = __builtin_ctz(n);
    ensure_base(zeros);
    int shift = base - zeros;
    for(int i = 0; i < n; i++) {
      if(i < (rev[i] >> shift)) {
        swap(a[i], a[rev[i] >> shift]);
      }
    }
    for(int k = 1; k < n; k <<= 1) {
      for(int i = 0; i < n; i += 2 * k) {
        for(int j = 0; j < k; j++) {
          Mint z = a[i + j + k] * rts[j + k];
          a[i + j + k] = a[i + j] - z;
          a[i + j] = a[i + j] + z;
        }
      }
    }
  }


  void intt(vector< Mint > &a) {
    const int n = (int) a.size();
    ntt(a);
    reverse(a.begin() + 1, a.end());
    Mint inv_sz = Mint(1) / n;
    for(int i = 0; i < n; i++) a[i] *= inv_sz;
  }

  vector< Mint > multiply(vector< Mint > a, vector< Mint > b) {
    int need = a.size() + b.size() - 1;
    int nbase = 1;
    while((1 << nbase) < need) nbase++;
    ensure_base(nbase);
    int sz = 1 << nbase;
    a.resize(sz, 0);
    b.resize(sz, 0);
    ntt(a);
    ntt(b);
    Mint inv_sz = Mint(1) / sz;
    for(int i = 0; i < sz; i++) {
      a[i] *= b[i] * inv_sz;
    }
    reverse(a.begin() + 1, a.end());
    ntt(a);
    a.resize(need);
    return a;
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

