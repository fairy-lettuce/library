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


# :heavy_check_mark: Kth-Root <small>(math/number-theory/kth-root.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#d4a327615e3a055131f0682831111ce2">math/number-theory</a>
* <a href="{{ site.github.repository_url }}/blob/master/math/number-theory/kth-root.cpp">View this file on GitHub</a>
    - Last commit date: 2020-03-03 18:40:18+09:00




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-kth-root-integer.test.cpp.html">test/verify/yosupo-kth-root-integer.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Kth-Root
 */
uint64_t kth_root(uint64_t a, int k) {
  if(k == 1) return a;
  auto check = [&](uint32_t x) {
    uint64_t mul = 1;
    for(int j = 0; j < k; j++) {
      if(__builtin_mul_overflow(mul, x, &mul)) return false;
    }
    return mul <= a;
  };
  uint64_t ret = 0;
  for(int i = 31; i >= 0; i--) {
    if(check(ret | (1u << i))) ret |= 1u << i;
  }
  return ret;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "math/number-theory/kth-root.cpp"
/**
 * @brief Kth-Root
 */
uint64_t kth_root(uint64_t a, int k) {
  if(k == 1) return a;
  auto check = [&](uint32_t x) {
    uint64_t mul = 1;
    for(int j = 0; j < k; j++) {
      if(__builtin_mul_overflow(mul, x, &mul)) return false;
    }
    return mul <= a;
  };
  uint64_t ret = 0;
  for(int i = 31; i >= 0; i--) {
    if(check(ret | (1u << i))) ret |= 1u << i;
  }
  return ret;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

