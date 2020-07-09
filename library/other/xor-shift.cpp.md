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


# :warning: Xor-Shift <small>(other/xor-shift.cpp)</small>

<a href="../../index.html">Back to top page</a>

* category: <a href="../../index.html#795f3202b17cb6bc3d4b771d8c6c9eaf">other</a>
* <a href="{{ site.github.repository_url }}/blob/master/other/xor-shift.cpp">View this file on GitHub</a>
    - Last commit date: 2020-07-10 00:47:43+09:00




## 概要
Xorshift は擬似乱数生成法の一つである.

周期が $2^{64}-1$ となる実装を示した.

* `XorShift(seed)`: シード値 `seed` で初期化する.
* `get()`: $[0, 2^{64})$ で生成した乱数を返す.
* `get(r)`: $[0, r)$ で生成した乱数を返す. `r` は32bit整数に限る. 64bitで生成したい場合は例えば `get()` を `r` で割った余りを求めるとよい.
* `get(l, r)`: $[l, r)$ で生成した乱数を返す.
* `probability()`: $[0.0, 1.0)$ で生成した乱数(実数)を返す.


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Xor-Shift
 * @docs docs/xor-shift.md
 */
struct XorShift {
private:
  constexpr static double R = 1.0 / 0xffffffff;
  uint64_t x;

public:
  explicit XorShift(uint64_t seed = 88172645463325252ull) : x(seed) {}

  template< typename T = uint64_t >
  inline T get() { // [0, 2^64)
    x ^= x << 7ull;
    x ^= x >> 9ull;
    return x;
  }

  inline uint32_t get(uint32_t r) { // [0, r)
    return ((uint64_t) get< uint32_t >() * r) >> 32ull;
  }

  inline uint32_t get(uint32_t l, uint32_t r) { // [l, r)
    return l + get(r - l);
  }

  inline double probability() { // [0.0, 1.0]
    return get< uint32_t >() * R;
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "other/xor-shift.cpp"
/**
 * @brief Xor-Shift
 * @docs docs/xor-shift.md
 */
struct XorShift {
private:
  constexpr static double R = 1.0 / 0xffffffff;
  uint64_t x;

public:
  explicit XorShift(uint64_t seed = 88172645463325252ull) : x(seed) {}

  template< typename T = uint64_t >
  inline T get() { // [0, 2^64)
    x ^= x << 7ull;
    x ^= x >> 9ull;
    return x;
  }

  inline uint32_t get(uint32_t r) { // [0, r)
    return ((uint64_t) get< uint32_t >() * r) >> 32ull;
  }

  inline uint32_t get(uint32_t l, uint32_t r) { // [l, r)
    return l + get(r - l);
  }

  inline double probability() { // [0.0, 1.0]
    return get< uint32_t >() * R;
  }
};

```
{% endraw %}

<a href="../../index.html">Back to top page</a>

