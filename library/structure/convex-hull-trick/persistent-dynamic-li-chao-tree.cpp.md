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


# :warning: structure/convex-hull-trick/persistent-dynamic-li-chao-tree.cpp
<a href="../../../index.html">Back to top page</a>

* category: structure/convex-hull-trick
* <a href="{{ site.github.repository_url }}/blob/master/structure/convex-hull-trick/persistent-dynamic-li-chao-tree.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 22:41:48 +0900




## Code
{% raw %}
```cpp
template< typename T, T x_low, T x_high, T id >
struct PersistentDynamicLiChaoTree {

  struct Line {
    T a, b;

    Line(T a, T b) : a(a), b(b) {}

    inline T get(T x) const { return a * x + b; }
  };

  struct Node {
    Line x;
    Node *l, *r;

    Node(const Line &x) : x{x}, l{nullptr}, r{nullptr} {}
  };

  Node *root;

  PersistentDynamicLiChaoTree() : root{nullptr} {}

  Node *update(Node *t, Line &x, const T &l, const T &r, const T &x_l, const T &x_r) {
    if(!t) return new Node(x);
    auto t_l = t->x.get(l), t_r = t->x.get(r);
    if(t_l <= x_l && t_r <= x_r) {
      return t;
    } else if(t_l >= x_l && t_r >= x_r) {
      t = new Node(*t);
      t->x = x;
      return t;
    } else {
      T m = (l + r) / 2;
      auto t_m = t->x.get(m), x_m = x.get(m);
      t = new Node(*t);
      if(t_m > x_m) {
        swap(t->x, x);
        if(x_l >= t_l) t->l = update(t->l, x, l, m, t_l, t_m);
        else t->r = update(t->r, x, m + 1, r, t_m + x.a, t_r);
      } else {
        if(t_l >= x_l) t->l = update(t->l, x, l, m, x_l, x_m);
        else t->r = update(t->r, x, m + 1, r, x_m + x.a, x_r);
      }
      return t;
    }
  }

  void update(const T &a, const T &b) {
    Line x(a, b);
    root = update(root, x, x_low, x_high, x.get(x_low), x.get(x_high));
  }

  T query(const Node *t, const T &l, const T &r, const T &x) const {
    if(!t) return id;
    if(l == r) return t->x.get(x);
    T m = (l + r) / 2;
    if(x <= m) return min(t->x.get(x), query(t->l, l, m, x));
    else return min(t->x.get(x), query(t->r, m + 1, r, x));
  }

  T query(const T &x) const {
    return query(root, x_low, x_high, x);
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

