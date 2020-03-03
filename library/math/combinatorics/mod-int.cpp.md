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


# :heavy_check_mark: math/combinatorics/mod-int.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#d319ed68764efb4f50b1628220df55d7">math/combinatorics</a>
* <a href="{{ site.github.repository_url }}/blob/master/math/combinatorics/mod-int.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 23:36:31+09:00




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-2405.test.cpp.html">test/verify/aoj-2405.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-dpl-5-g.test.cpp.html">test/verify/aoj-dpl-5-g.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-dpl-5-i.test.cpp.html">test/verify/aoj-dpl-5-i.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-dpl-5-j.test.cpp.html">test/verify/aoj-dpl-5-j.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-bellnoulli-number.test.cpp.html">test/verify/yosupo-bellnoulli-number.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-exp-of-formal-power-series.test.cpp.html">test/verify/yosupo-exp-of-formal-power-series.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-find-linear-recurrence.test.cpp.html">test/verify/yosupo-find-linear-recurrence.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-inv-of-formal-power-series.test.cpp.html">test/verify/yosupo-inv-of-formal-power-series.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-log-of-formal-power-series.test.cpp.html">test/verify/yosupo-log-of-formal-power-series.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-matrix-det.test.cpp.html">test/verify/yosupo-matrix-det.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-multipoint-evaluation.test.cpp.html">test/verify/yosupo-multipoint-evaluation.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-partition-function.test.cpp.html">test/verify/yosupo-partition-function.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-polynomial-interpolation.test.cpp.html">test/verify/yosupo-polynomial-interpolation.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-sparse-matrix-det.test.cpp.html">test/verify/yosupo-sparse-matrix-det.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-sqrt-of-formal-power-series.test.cpp.html">test/verify/yosupo-sqrt-of-formal-power-series.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
template< int mod >
struct ModInt {
  int x;

  ModInt() : x(0) {}

  ModInt(int64_t y) : x(y >= 0 ? y % mod : (mod - (-y) % mod) % mod) {}

  ModInt &operator+=(const ModInt &p) {
    if((x += p.x) >= mod) x -= mod;
    return *this;
  }

  ModInt &operator-=(const ModInt &p) {
    if((x += mod - p.x) >= mod) x -= mod;
    return *this;
  }

  ModInt &operator*=(const ModInt &p) {
    x = (int) (1LL * x * p.x % mod);
    return *this;
  }

  ModInt &operator/=(const ModInt &p) {
    *this *= p.inverse();
    return *this;
  }

  ModInt operator-() const { return ModInt(-x); }

  ModInt operator+(const ModInt &p) const { return ModInt(*this) += p; }

  ModInt operator-(const ModInt &p) const { return ModInt(*this) -= p; }

  ModInt operator*(const ModInt &p) const { return ModInt(*this) *= p; }

  ModInt operator/(const ModInt &p) const { return ModInt(*this) /= p; }

  bool operator==(const ModInt &p) const { return x == p.x; }

  bool operator!=(const ModInt &p) const { return x != p.x; }

  ModInt inverse() const {
    int a = x, b = mod, u = 1, v = 0, t;
    while(b > 0) {
      t = a / b;
      swap(a -= t * b, b);
      swap(u -= t * v, v);
    }
    return ModInt(u);
  }

  ModInt pow(int64_t n) const {
    ModInt ret(1), mul(x);
    while(n > 0) {
      if(n & 1) ret *= mul;
      mul *= mul;
      n >>= 1;
    }
    return ret;
  }

  friend ostream &operator<<(ostream &os, const ModInt &p) {
    return os << p.x;
  }

  friend istream &operator>>(istream &is, ModInt &a) {
    int64_t t;
    is >> t;
    a = ModInt< mod >(t);
    return (is);
  }

  static int get_mod() { return mod; }
};

using modint = ModInt< mod >;

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "math/combinatorics/mod-int.cpp"
template< int mod >
struct ModInt {
  int x;

  ModInt() : x(0) {}

  ModInt(int64_t y) : x(y >= 0 ? y % mod : (mod - (-y) % mod) % mod) {}

  ModInt &operator+=(const ModInt &p) {
    if((x += p.x) >= mod) x -= mod;
    return *this;
  }

  ModInt &operator-=(const ModInt &p) {
    if((x += mod - p.x) >= mod) x -= mod;
    return *this;
  }

  ModInt &operator*=(const ModInt &p) {
    x = (int) (1LL * x * p.x % mod);
    return *this;
  }

  ModInt &operator/=(const ModInt &p) {
    *this *= p.inverse();
    return *this;
  }

  ModInt operator-() const { return ModInt(-x); }

  ModInt operator+(const ModInt &p) const { return ModInt(*this) += p; }

  ModInt operator-(const ModInt &p) const { return ModInt(*this) -= p; }

  ModInt operator*(const ModInt &p) const { return ModInt(*this) *= p; }

  ModInt operator/(const ModInt &p) const { return ModInt(*this) /= p; }

  bool operator==(const ModInt &p) const { return x == p.x; }

  bool operator!=(const ModInt &p) const { return x != p.x; }

  ModInt inverse() const {
    int a = x, b = mod, u = 1, v = 0, t;
    while(b > 0) {
      t = a / b;
      swap(a -= t * b, b);
      swap(u -= t * v, v);
    }
    return ModInt(u);
  }

  ModInt pow(int64_t n) const {
    ModInt ret(1), mul(x);
    while(n > 0) {
      if(n & 1) ret *= mul;
      mul *= mul;
      n >>= 1;
    }
    return ret;
  }

  friend ostream &operator<<(ostream &os, const ModInt &p) {
    return os << p.x;
  }

  friend istream &operator>>(istream &is, ModInt &a) {
    int64_t t;
    is >> t;
    a = ModInt< mod >(t);
    return (is);
  }

  static int get_mod() { return mod; }
};

using modint = ModInt< mod >;

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

