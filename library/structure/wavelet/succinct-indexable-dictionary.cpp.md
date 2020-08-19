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


# :heavy_check_mark: structure/wavelet/succinct-indexable-dictionary.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5f498e54a9680c92dbc18487ab14a24d">structure/wavelet</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/wavelet/succinct-indexable-dictionary.cpp">View this file on GitHub</a>
    - Last commit date: 2019-12-31 16:31:54+09:00




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-1549-2.test.cpp.html">test/verify/aoj-1549-2.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-1549.test.cpp.html">test/verify/aoj-1549.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-2674-2.test.cpp.html">test/verify/aoj-2674-2.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-2674.test.cpp.html">test/verify/aoj-2674.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-point-add-rectangle-sum.test.cpp.html">test/verify/yosupo-point-add-rectangle-sum.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-range-kth-smallest-2.test.cpp.html">test/verify/yosupo-range-kth-smallest-2.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-range-kth-smallest.test.cpp.html">test/verify/yosupo-range-kth-smallest.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-rectangle-sum.test.cpp.html">test/verify/yosupo-rectangle-sum.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
struct SuccinctIndexableDictionary {
  size_t length;
  size_t blocks;
  vector< unsigned > bit, sum;

  SuccinctIndexableDictionary() = default;

  SuccinctIndexableDictionary(size_t length) : length(length), blocks((length + 31) >> 5) {
    bit.assign(blocks, 0U);
    sum.assign(blocks, 0U);
  }

  void set(int k) {
    bit[k >> 5] |= 1U << (k & 31);
  }

  void build() {
    sum[0] = 0U;
    for(int i = 1; i < blocks; i++) {
      sum[i] = sum[i - 1] + __builtin_popcount(bit[i - 1]);
    }
  }

  bool operator[](int k) {
    return (bool((bit[k >> 5] >> (k & 31)) & 1));
  }

  int rank(int k) {
    return (sum[k >> 5] + __builtin_popcount(bit[k >> 5] & ((1U << (k & 31)) - 1)));
  }

  int rank(bool val, int k) {
    return (val ? rank(k) : k - rank(k));
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/wavelet/succinct-indexable-dictionary.cpp"
struct SuccinctIndexableDictionary {
  size_t length;
  size_t blocks;
  vector< unsigned > bit, sum;

  SuccinctIndexableDictionary() = default;

  SuccinctIndexableDictionary(size_t length) : length(length), blocks((length + 31) >> 5) {
    bit.assign(blocks, 0U);
    sum.assign(blocks, 0U);
  }

  void set(int k) {
    bit[k >> 5] |= 1U << (k & 31);
  }

  void build() {
    sum[0] = 0U;
    for(int i = 1; i < blocks; i++) {
      sum[i] = sum[i - 1] + __builtin_popcount(bit[i - 1]);
    }
  }

  bool operator[](int k) {
    return (bool((bit[k >> 5] >> (k & 31)) & 1));
  }

  int rank(int k) {
    return (sum[k >> 5] + __builtin_popcount(bit[k >> 5] & ((1U << (k & 31)) - 1)));
  }

  int rank(bool val, int k) {
    return (val ? rank(k) : k - rank(k));
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

