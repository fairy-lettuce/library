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


# :heavy_check_mark: structure/convex-hull-trick/dynamic-li-chao-tree.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#3ad23896bbde10d07ed9c44a914e070b">structure/convex-hull-trick</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/convex-hull-trick/dynamic-li-chao-tree.cpp">View this file on GitHub</a>
    - Last commit date: 2020-01-07 02:07:19+09:00




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-line-add-get-min.test.cpp.html">test/verify/yosupo-line-add-get-min.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-segment-add-get-min.test.cpp.html">test/verify/yosupo-segment-add-get-min.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
template< typename T, T x_low, T x_high, T id >
struct DynamicLiChaoTree {

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

  DynamicLiChaoTree() : root{nullptr} {}

  Node *add_line(Node *t, Line &x, const T &l, const T &r, const T &x_l, const T &x_r) {
    if(!t) return new Node(x);

    T t_l = t->x.get(l), t_r = t->x.get(r);

    if(t_l <= x_l && t_r <= x_r) {
      return t;
    } else if(t_l >= x_l && t_r >= x_r) {
      t->x = x;
      return t;
    } else {
      T m = (l + r) / 2;
      if(m == r) --m;
      T t_m = t->x.get(m), x_m = x.get(m);
      if(t_m > x_m) {
        swap(t->x, x);
        if(x_l >= t_l) t->l = add_line(t->l, x, l, m, t_l, t_m);
        else t->r = add_line(t->r, x, m + 1, r, t_m + x.a, t_r);
      } else {
        if(t_l >= x_l) t->l = add_line(t->l, x, l, m, x_l, x_m);
        else t->r = add_line(t->r, x, m + 1, r, x_m + x.a, x_r);
      }
      return t;
    }
  }

  void add_line(const T &a, const T &b) {
    Line x(a, b);
    root = add_line(root, x, x_low, x_high, x.get(x_low), x.get(x_high));
  }

  Node *add_segment(Node *t, Line &x, const T &a, const T &b, const T &l, const T &r, const T &x_l, const T &x_r) {
    if(r < a || b < l) return t;
    if(a <= l && r <= b) {
      Line y{x};
      return add_line(t, y, l, r, x_l, x_r);
    }
    if(t) {
      T t_l = t->x.get(l), t_r = t->x.get(r);
      if(t_l <= x_l && t_r <= x_r) return t;
    } else {
      t = new Node(Line(0, id));
    }
    T m = (l + r) / 2;
    if(m == r) --m;
    T x_m = x.get(m);
    t->l = add_segment(t->l, x, a, b, l, m, x_l, x_m);
    t->r = add_segment(t->r, x, a, b, m + 1, r, x_m + x.a, x_r);
    return t;
  }

  void add_segment(const T &l, const T &r, const T &a, const T &b) {
    Line x(a, b);
    root = add_segment(root, x, l, r - 1, x_low, x_high, x.get(x_low), x.get(x_high));
  }

  T query(const Node *t, const T &l, const T &r, const T &x) const {
    if(!t) return id;
    if(l == r) return t->x.get(x);
    T m = (l + r) / 2;
    if(m == r) --m;
    if(x <= m) return min(t->x.get(x), query(t->l, l, m, x));
    else return min(t->x.get(x), query(t->r, m + 1, r, x));
  }

  T query(const T &x) const {
    return query(root, x_low, x_high, x);
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/convex-hull-trick/dynamic-li-chao-tree.cpp"
template< typename T, T x_low, T x_high, T id >
struct DynamicLiChaoTree {

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

  DynamicLiChaoTree() : root{nullptr} {}

  Node *add_line(Node *t, Line &x, const T &l, const T &r, const T &x_l, const T &x_r) {
    if(!t) return new Node(x);

    T t_l = t->x.get(l), t_r = t->x.get(r);

    if(t_l <= x_l && t_r <= x_r) {
      return t;
    } else if(t_l >= x_l && t_r >= x_r) {
      t->x = x;
      return t;
    } else {
      T m = (l + r) / 2;
      if(m == r) --m;
      T t_m = t->x.get(m), x_m = x.get(m);
      if(t_m > x_m) {
        swap(t->x, x);
        if(x_l >= t_l) t->l = add_line(t->l, x, l, m, t_l, t_m);
        else t->r = add_line(t->r, x, m + 1, r, t_m + x.a, t_r);
      } else {
        if(t_l >= x_l) t->l = add_line(t->l, x, l, m, x_l, x_m);
        else t->r = add_line(t->r, x, m + 1, r, x_m + x.a, x_r);
      }
      return t;
    }
  }

  void add_line(const T &a, const T &b) {
    Line x(a, b);
    root = add_line(root, x, x_low, x_high, x.get(x_low), x.get(x_high));
  }

  Node *add_segment(Node *t, Line &x, const T &a, const T &b, const T &l, const T &r, const T &x_l, const T &x_r) {
    if(r < a || b < l) return t;
    if(a <= l && r <= b) {
      Line y{x};
      return add_line(t, y, l, r, x_l, x_r);
    }
    if(t) {
      T t_l = t->x.get(l), t_r = t->x.get(r);
      if(t_l <= x_l && t_r <= x_r) return t;
    } else {
      t = new Node(Line(0, id));
    }
    T m = (l + r) / 2;
    if(m == r) --m;
    T x_m = x.get(m);
    t->l = add_segment(t->l, x, a, b, l, m, x_l, x_m);
    t->r = add_segment(t->r, x, a, b, m + 1, r, x_m + x.a, x_r);
    return t;
  }

  void add_segment(const T &l, const T &r, const T &a, const T &b) {
    Line x(a, b);
    root = add_segment(root, x, l, r - 1, x_low, x_high, x.get(x_low), x.get(x_high));
  }

  T query(const Node *t, const T &l, const T &r, const T &x) const {
    if(!t) return id;
    if(l == r) return t->x.get(x);
    T m = (l + r) / 2;
    if(m == r) --m;
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

