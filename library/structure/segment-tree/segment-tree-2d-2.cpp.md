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


# :warning: structure/segment-tree/segment-tree-2d-2.cpp
<a href="../../../index.html">Back to top page</a>

* category: structure/segment-tree
* <a href="{{ site.github.repository_url }}/blob/master/structure/segment-tree/segment-tree-2d-2.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 22:41:48 +0900




## Code
{% raw %}
```cpp
template< typename structure_t, typename get_t, typename update_t >
struct SegmentTree2D {
  using merge_f = function< get_t(get_t, get_t) >;
  using get_t = function< get_t(structure_t &, int) >;
  using range_update_f = function< get_t(structure_t &, int, int, update_t) >;

  int sz;
  vector< structure_t > seg;
  const merge_f &f;
  const get_t &g;
  const range_update_f &h;

  SegmentTree2D(int n, const merge_f &f, const get_t &g, const range_update_f &h) : f(f), g(g), h(h) {
    sz = 1;
    while(sz < n) sz <<= 1;
    seg.resize(2 * sz - 1);
  }

  void update(int a, int b, int lower, int upper, update_t x, int k, int l, int r) {
    if(r <= a || b <= l) {
      return;
    } else if(a <= l && r <= b) {
      g(seg[k], lower, upper, x);
    } else {
      update(a, b, lower, upper, x, 2 * k + 1, l, (l + r) >> 1);
      update(a, b, lower, upper, x, 2 * k + 2, (l + r) >> 1, r);
    }
  }

  void update(int a, int b, int l, int r, update_t x) {
    update(a, b, l, r, x, 0, 0, sz);
  }

  get_t get(int x, int y) {
    x += sz - 1;
    get_t ret = g(seg[x], y);
    while(x > 0) {
      x = (x - 1) >> 1;
      ret = f(ret, g(seg[x], y));
    }
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

