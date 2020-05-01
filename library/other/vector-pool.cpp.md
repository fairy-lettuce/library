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


# :question: other/vector-pool.cpp

<a href="../../index.html">Back to top page</a>

* category: <a href="../../index.html#795f3202b17cb6bc3d4b771d8c6c9eaf">other</a>
* <a href="{{ site.github.repository_url }}/blob/master/other/vector-pool.cpp">View this file on GitHub</a>
    - Last commit date: 2020-04-26 00:10:50+09:00




## Verified with

* :heavy_check_mark: <a href="../../verify/test/verify/aoj-1508-2.test.cpp.html">test/verify/aoj-1508-2.test.cpp</a>
* :x: <a href="../../verify/test/verify/yosupo-range-affine-range-sum-2.test.cpp.html">test/verify/yosupo-range-affine-range-sum-2.test.cpp</a>
* :heavy_check_mark: <a href="../../verify/test/verify/yosupo-staticrmq-3.test.cpp.html">test/verify/yosupo-staticrmq-3.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
template< class T >
struct VectorPool {
  vector< T > pool;
  vector< T * > stock;
  int ptr;

  VectorPool() = default;

  VectorPool(int sz) : pool(sz), stock(sz) {}

  inline T *alloc() { return stock[--ptr]; }

  inline void free(T *t) { stock[ptr++] = t; }

  void clear() {
    ptr = (int) pool.size();
    for(int i = 0; i < pool.size(); i++) stock[i] = &pool[i];
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "other/vector-pool.cpp"
template< class T >
struct VectorPool {
  vector< T > pool;
  vector< T * > stock;
  int ptr;

  VectorPool() = default;

  VectorPool(int sz) : pool(sz), stock(sz) {}

  inline T *alloc() { return stock[--ptr]; }

  inline void free(T *t) { stock[ptr++] = t; }

  void clear() {
    ptr = (int) pool.size();
    for(int i = 0; i < pool.size(); i++) stock[i] = &pool[i];
  }
};

```
{% endraw %}

<a href="../../index.html">Back to top page</a>

