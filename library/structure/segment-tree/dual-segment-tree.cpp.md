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


# :heavy_check_mark: Dual-Segment-Tree(双対セグメント木) <small>(structure/segment-tree/dual-segment-tree.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#bd066fce418dc5d58690e9bbe0a7a21f">structure/segment-tree</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/segment-tree/dual-segment-tree.cpp">View this file on GitHub</a>
    - Last commit date: 2020-02-20 22:23:04+09:00




## 概要

* `DualSegmentTree(n, h, OM0)`: サイズ `n` で初期化する. ここで `h` は2つの区間の作用素をマージする二項演算, `OM0` は作用素の単位元である.
* `update(l, r, x)`: 区間 $[l, r)$ に作用素 `x` を適用する.
* `operator[k]`: `k` 番目の作用素を返す.


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-dsl-2-d.test.cpp.html">test/verify/aoj-dsl-2-d.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Dual-Segment-Tree(双対セグメント木)
 * @docs docs/dual-segment-tree.md
 */
template< typename OperatorMonoid >
struct DualSegmentTree {
  using H = function< OperatorMonoid(OperatorMonoid, OperatorMonoid) >;

  int sz, height;
  vector< OperatorMonoid > lazy;
  const H h;
  const OperatorMonoid OM0;

  DualSegmentTree(int n, const H h, const OperatorMonoid &OM0) : h(h), OM0(OM0) {
    sz = 1;
    height = 0;
    while(sz < n) sz <<= 1, height++;
    lazy.assign(2 * sz, OM0);
  }

  inline void propagate(int k) {
    if(lazy[k] != OM0) {
      lazy[2 * k + 0] = h(lazy[2 * k + 0], lazy[k]);
      lazy[2 * k + 1] = h(lazy[2 * k + 1], lazy[k]);
      lazy[k] = OM0;
    }
  }

  inline void thrust(int k) {
    for(int i = height; i > 0; i--) propagate(k >> i);
  }

  void update(int a, int b, const OperatorMonoid &x) {
    thrust(a += sz);
    thrust(b += sz - 1);
    for(int l = a, r = b + 1; l < r; l >>= 1, r >>= 1) {
      if(l & 1) lazy[l] = h(lazy[l], x), ++l;
      if(r & 1) --r, lazy[r] = h(lazy[r], x);
    }
  }

  OperatorMonoid operator[](int k) {
    thrust(k += sz);
    return lazy[k];
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/segment-tree/dual-segment-tree.cpp"
/**
 * @brief Dual-Segment-Tree(双対セグメント木)
 * @docs docs/dual-segment-tree.md
 */
template< typename OperatorMonoid >
struct DualSegmentTree {
  using H = function< OperatorMonoid(OperatorMonoid, OperatorMonoid) >;

  int sz, height;
  vector< OperatorMonoid > lazy;
  const H h;
  const OperatorMonoid OM0;

  DualSegmentTree(int n, const H h, const OperatorMonoid &OM0) : h(h), OM0(OM0) {
    sz = 1;
    height = 0;
    while(sz < n) sz <<= 1, height++;
    lazy.assign(2 * sz, OM0);
  }

  inline void propagate(int k) {
    if(lazy[k] != OM0) {
      lazy[2 * k + 0] = h(lazy[2 * k + 0], lazy[k]);
      lazy[2 * k + 1] = h(lazy[2 * k + 1], lazy[k]);
      lazy[k] = OM0;
    }
  }

  inline void thrust(int k) {
    for(int i = height; i > 0; i--) propagate(k >> i);
  }

  void update(int a, int b, const OperatorMonoid &x) {
    thrust(a += sz);
    thrust(b += sz - 1);
    for(int l = a, r = b + 1; l < r; l >>= 1, r >>= 1) {
      if(l & 1) lazy[l] = h(lazy[l], x), ++l;
      if(r & 1) --r, lazy[r] = h(lazy[r], x);
    }
  }

  OperatorMonoid operator[](int k) {
    thrust(k += sz);
    return lazy[k];
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

