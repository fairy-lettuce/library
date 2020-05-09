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


# :heavy_check_mark: Rolling-Hash(ローリングハッシュ) <small>(string/rolling-hash.cpp)</small>

<a href="../../index.html">Back to top page</a>

* category: <a href="../../index.html#b45cffe084dd3d20d928bee85e7b0f21">string</a>
* <a href="{{ site.github.repository_url }}/blob/master/string/rolling-hash.cpp">View this file on GitHub</a>
    - Last commit date: 2020-05-09 22:53:41+09:00


* see: <a href="https://qiita.com/keymoon/items/11fac5627672a6d6a9f6">https://qiita.com/keymoon/items/11fac5627672a6d6a9f6</a>


## Verified with

* :heavy_check_mark: <a href="../../verify/test/verify/aoj-alds-1-14-b.test.cpp.html">test/verify/aoj-alds-1-14-b.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Rolling-Hash(ローリングハッシュ)
 * @see https://qiita.com/keymoon/items/11fac5627672a6d6a9f6
 */
struct RollingHash {
  static const uint64_t mod = (1ull << 61ull) - 1;
  using uint128_t = __uint128_t;
  vector< uint64_t > hashed, power;
  const uint64_t base;

  static inline uint64_t add(uint64_t a, uint64_t b) {
    if((a += b) >= mod) a -= mod;
    return a;
  }

  static inline uint64_t mul(uint64_t a, uint64_t b) {
    uint128_t c = (uint128_t) a * b;
    return add(c >> 61, c & mod);
  }

  static inline uint64_t generate_base() {
    mt19937_64 mt(chrono::steady_clock::now().time_since_epoch().count());
    uniform_int_distribution< uint64_t > rand(1, RollingHash::mod - 1);
    return rand(mt);
  }

  RollingHash() = default;

  RollingHash(const string &s, uint64_t base) : base(base) {
    size_t sz = s.size();
    hashed.assign(sz + 1, 0);
    power.assign(sz + 1, 0);
    power[0] = 1;
    for(int i = 0; i < sz; i++) {
      power[i + 1] = mul(power[i], base);
      hashed[i + 1] = add(mul(hashed[i], base), s[i]);
    }
  }

  template< typename T >
  RollingHash(const vector< T > &s, uint64_t base) : base(base) {
    size_t sz = s.size();
    hashed.assign(sz + 1, 0);
    power.assign(sz + 1, 0);
    power[0] = 1;
    for(int i = 0; i < sz; i++) {
      power[i + 1] = mul(power[i], base);
      hashed[i + 1] = add(mul(hashed[i], base), s[i]);
    }
  }

  uint64_t query(int l, int r) const {
    return add(hashed[r], mod - mul(hashed[l], power[r - l]));
  }

  uint64_t combine(uint64_t h1, uint64_t h2, size_t h2len) const {
    return add(mul(h1, power[h2len]), h2);
  }

  int lcp(const RollingHash &b, int l1, int r1, int l2, int r2) const {
    assert(base == b.base);
    int len = min(r1 - l1, r2 - l2);
    int low = 0, high = len + 1;
    while(high - low > 1) {
      int mid = (low + high) / 2;
      if(query(l1, l1 + mid) == b.query(l2, l2 + mid)) low = mid;
      else high = mid;
    }
    return low;
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "string/rolling-hash.cpp"
/**
 * @brief Rolling-Hash(ローリングハッシュ)
 * @see https://qiita.com/keymoon/items/11fac5627672a6d6a9f6
 */
struct RollingHash {
  static const uint64_t mod = (1ull << 61ull) - 1;
  using uint128_t = __uint128_t;
  vector< uint64_t > hashed, power;
  const uint64_t base;

  static inline uint64_t add(uint64_t a, uint64_t b) {
    if((a += b) >= mod) a -= mod;
    return a;
  }

  static inline uint64_t mul(uint64_t a, uint64_t b) {
    uint128_t c = (uint128_t) a * b;
    return add(c >> 61, c & mod);
  }

  static inline uint64_t generate_base() {
    mt19937_64 mt(chrono::steady_clock::now().time_since_epoch().count());
    uniform_int_distribution< uint64_t > rand(1, RollingHash::mod - 1);
    return rand(mt);
  }

  RollingHash() = default;

  RollingHash(const string &s, uint64_t base) : base(base) {
    size_t sz = s.size();
    hashed.assign(sz + 1, 0);
    power.assign(sz + 1, 0);
    power[0] = 1;
    for(int i = 0; i < sz; i++) {
      power[i + 1] = mul(power[i], base);
      hashed[i + 1] = add(mul(hashed[i], base), s[i]);
    }
  }

  template< typename T >
  RollingHash(const vector< T > &s, uint64_t base) : base(base) {
    size_t sz = s.size();
    hashed.assign(sz + 1, 0);
    power.assign(sz + 1, 0);
    power[0] = 1;
    for(int i = 0; i < sz; i++) {
      power[i + 1] = mul(power[i], base);
      hashed[i + 1] = add(mul(hashed[i], base), s[i]);
    }
  }

  uint64_t query(int l, int r) const {
    return add(hashed[r], mod - mul(hashed[l], power[r - l]));
  }

  uint64_t combine(uint64_t h1, uint64_t h2, size_t h2len) const {
    return add(mul(h1, power[h2len]), h2);
  }

  int lcp(const RollingHash &b, int l1, int r1, int l2, int r2) const {
    assert(base == b.base);
    int len = min(r1 - l1, r2 - l2);
    int low = 0, high = len + 1;
    while(high - low > 1) {
      int mid = (low + high) / 2;
      if(query(l1, l1 + mid) == b.query(l2, l2 + mid)) low = mid;
      else high = mid;
    }
    return low;
  }
};

```
{% endraw %}

<a href="../../index.html">Back to top page</a>

