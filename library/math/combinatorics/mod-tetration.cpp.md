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


# :heavy_check_mark: Mod-Tetration <small>(math/combinatorics/mod-tetration.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#d319ed68764efb4f50b1628220df55d7">math/combinatorics</a>
* <a href="{{ site.github.repository_url }}/blob/master/math/combinatorics/mod-tetration.cpp">View this file on GitHub</a>
    - Last commit date: 2020-03-03 18:28:13+09:00




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-tetration-mod.test.cpp.html">test/verify/yosupo-tetration-mod.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Mod-Tetration
 */
template< typename T >
T mod_tetration(const T &a, const T &b, const T &m) {
  if(m == 1) return 0;
  if(a == 0) return !(b & 1);
  if(b == 0) return 1;
  if(b == 1) return a % m;
  if(b == 2) return mod_pow(a % m, a, m);
  auto phi = euler_phi(m);
  return mod_pow(a % m, mod_tetration(a, b - 1, phi) + phi, m);
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "math/combinatorics/mod-tetration.cpp"
/**
 * @brief Mod-Tetration
 */
template< typename T >
T mod_tetration(const T &a, const T &b, const T &m) {
  if(m == 1) return 0;
  if(a == 0) return !(b & 1);
  if(b == 0) return 1;
  if(b == 1) return a % m;
  if(b == 2) return mod_pow(a % m, a, m);
  auto phi = euler_phi(m);
  return mod_pow(a % m, mod_tetration(a, b - 1, phi) + phi, m);
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

