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


# :warning: structure/segment-tree/dual-segment-tree.cpp
<a href="../../../index.html">Back to top page</a>

* category: structure/segment-tree
* <a href="{{ site.github.repository_url }}/blob/master/structure/segment-tree/dual-segment-tree.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 22:41:48 +0900




## Code
{% raw %}
```cpp
template< typename OperatorMonoid >
struct DualSegmentTree {
  using H = function< OperatorMonoid(OperatorMonoid, OperatorMonoid) >;

  int sz, height;
  vector< OperatorMonoid > lazy;
  const H h;
  const OperatorMonoid OM0;


  DualSegmentTree(int n, const H h, const OperatorMonoid OM0)
      : h(h), OM0(OM0) {
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

