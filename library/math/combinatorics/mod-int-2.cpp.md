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


# :warning: math/combinatorics/mod-int-2.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#d319ed68764efb4f50b1628220df55d7">math/combinatorics</a>
* <a href="{{ site.github.repository_url }}/blob/master/math/combinatorics/mod-int-2.cpp">View this file on GitHub</a>
    - Last commit date: 2020-01-22 22:52:06+09:00




## Code

<a id="unbundled"></a>
{% raw %}
```cpp
static constexpr uint32_t mul_inv(uint32_t n, int e = 5, uint32_t x = 1) {
  return e == 0 ? x : mul_inv(n, e - 1, x * (2 - x * n));
}

template< uint32_t mod, bool fast = false >
struct ModInt2 {
  using u32 = uint32_t;
  using u64 = uint64_t;

  static constexpr u32 inv = mul_inv(mod);
  static constexpr u32 r2 = -uint64_t(mod) % mod;

  uint32_t x;

  ModInt2() : x(0) {}

  ModInt2(const int64_t &y)
      : x(reduce(u64(fast ? y : (y >= 0 ? y % mod : (mod - (-y) % mod) % mod)) * r2)) {}

  u32 reduce(const u64 &w) const {
    return u32(w >> 32) + mod - u32((u64(u32(w) * inv) * mod) >> 32);
  }

  ModInt2 &operator+=(const ModInt2 &p) {
    if(int(x += p.x - 2 * mod) < 0) x += 2 * mod;
    return *this;
  }

  ModInt2 &operator-=(const ModInt2 &p) {
    if(int(x -= p.x) < 0) x += 2 * mod;
    return *this;
  }

  ModInt2 &operator*=(const ModInt2 &p) {
    x = reduce(uint64_t(x) * p.x);
    return *this;
  }

  ModInt2 &operator/=(const ModInt2 &p) {
    *this *= p.inverse();
    return *this;
  }

  ModInt2 operator-() const { return ModInt2() - *this; }

  ModInt2 operator+(const ModInt2 &p) const { return ModInt2(*this) += p; }

  ModInt2 operator-(const ModInt2 &p) const { return ModInt2(*this) -= p; }

  ModInt2 operator*(const ModInt2 &p) const { return ModInt2(*this) *= p; }

  ModInt2 operator/(const ModInt2 &p) const { return ModInt2(*this) /= p; }

  bool operator==(const ModInt2 &p) const { return get() == p.get(); }

  bool operator!=(const ModInt2 &p) const { return get() != p.get(); }

  int get() const { return reduce(x) % mod; }

  ModInt2 pow(int64_t n) const {
    ModInt2 ret(1), mul(*this);
    while(n > 0) {
      if(n & 1) ret *= mul;
      mul *= mul;
      n >>= 1;
    }
    return ret;
  }

  ModInt2 inverse() const {
    return pow(mod - 2);
  }

  friend ostream &operator<<(ostream &os, const ModInt2 &p) {
    return os << p.get();
  }

  friend istream &operator>>(istream &is, ModInt2 &a) {
    int64_t t;
    is >> t;
    a = ModInt2< mod, fast >(t);
    return (is);
  }

  static int get_mod() { return mod; }
};

using modint = ModInt2< mod >;

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "math/combinatorics/mod-int-2.cpp"
static constexpr uint32_t mul_inv(uint32_t n, int e = 5, uint32_t x = 1) {
  return e == 0 ? x : mul_inv(n, e - 1, x * (2 - x * n));
}

template< uint32_t mod, bool fast = false >
struct ModInt2 {
  using u32 = uint32_t;
  using u64 = uint64_t;

  static constexpr u32 inv = mul_inv(mod);
  static constexpr u32 r2 = -uint64_t(mod) % mod;

  uint32_t x;

  ModInt2() : x(0) {}

  ModInt2(const int64_t &y)
      : x(reduce(u64(fast ? y : (y >= 0 ? y % mod : (mod - (-y) % mod) % mod)) * r2)) {}

  u32 reduce(const u64 &w) const {
    return u32(w >> 32) + mod - u32((u64(u32(w) * inv) * mod) >> 32);
  }

  ModInt2 &operator+=(const ModInt2 &p) {
    if(int(x += p.x - 2 * mod) < 0) x += 2 * mod;
    return *this;
  }

  ModInt2 &operator-=(const ModInt2 &p) {
    if(int(x -= p.x) < 0) x += 2 * mod;
    return *this;
  }

  ModInt2 &operator*=(const ModInt2 &p) {
    x = reduce(uint64_t(x) * p.x);
    return *this;
  }

  ModInt2 &operator/=(const ModInt2 &p) {
    *this *= p.inverse();
    return *this;
  }

  ModInt2 operator-() const { return ModInt2() - *this; }

  ModInt2 operator+(const ModInt2 &p) const { return ModInt2(*this) += p; }

  ModInt2 operator-(const ModInt2 &p) const { return ModInt2(*this) -= p; }

  ModInt2 operator*(const ModInt2 &p) const { return ModInt2(*this) *= p; }

  ModInt2 operator/(const ModInt2 &p) const { return ModInt2(*this) /= p; }

  bool operator==(const ModInt2 &p) const { return get() == p.get(); }

  bool operator!=(const ModInt2 &p) const { return get() != p.get(); }

  int get() const { return reduce(x) % mod; }

  ModInt2 pow(int64_t n) const {
    ModInt2 ret(1), mul(*this);
    while(n > 0) {
      if(n & 1) ret *= mul;
      mul *= mul;
      n >>= 1;
    }
    return ret;
  }

  ModInt2 inverse() const {
    return pow(mod - 2);
  }

  friend ostream &operator<<(ostream &os, const ModInt2 &p) {
    return os << p.get();
  }

  friend istream &operator>>(istream &is, ModInt2 &a) {
    int64_t t;
    is >> t;
    a = ModInt2< mod, fast >(t);
    return (is);
  }

  static int get_mod() { return mod; }
};

using modint = ModInt2< mod >;

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

