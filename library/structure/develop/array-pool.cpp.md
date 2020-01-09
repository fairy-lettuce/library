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


# :heavy_check_mark: structure/develop/array-pool.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#b1cd1e8cabf258d1ad55a5bb477f1b01">structure/develop</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/develop/array-pool.cpp">View this file on GitHub</a>
    - Last commit date: 2020-01-09 17:25:25+09:00




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-2667.test.cpp.html">test/verify/aoj-2667.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
template< class T, size_t V >
struct ArrayPool {
  array< T, V > pool;
  array< T *, V > stock;
  int ptr;

  ArrayPool() { clear(); }

  inline T *alloc() {
    return stock[--ptr];
  }

  inline void free(T *t) {
    stock[ptr++] = t;
  }

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
#line 1 "structure/develop/array-pool.cpp"
template< class T, size_t V >
struct ArrayPool {
  array< T, V > pool;
  array< T *, V > stock;
  int ptr;

  ArrayPool() { clear(); }

  inline T *alloc() {
    return stock[--ptr];
  }

  inline void free(T *t) {
    stock[ptr++] = t;
  }

  void clear() {
    ptr = (int) pool.size();
    for(int i = 0; i < pool.size(); i++) stock[i] = &pool[i];
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

