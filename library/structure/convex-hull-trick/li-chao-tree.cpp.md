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


# :warning: structure/convex-hull-trick/li-chao-tree.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#3ad23896bbde10d07ed9c44a914e070b">structure/convex-hull-trick</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/convex-hull-trick/li-chao-tree.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 22:41:48+09:00




## Code

<a id="unbundled"></a>
{% raw %}
```cpp
template< typename T >
struct LiChaoTree {
  struct Line {
    T a, b;

    Line(T a, T b) : a(a), b(b) {}

    inline T get(T x) const { return a * x + b; }

    inline bool over(const Line &b, const T &x) const {
      return get(x) < b.get(x);
    }
  };

  vector< T > xs;
  vector< Line > seg;
  int sz;

  LiChaoTree(const vector< T > &x, T INF) : xs(x) {
    sz = 1;
    while(sz < xs.size()) sz <<= 1;
    while(xs.size() < sz) xs.push_back(xs.back() + 1);
    seg.assign(2 * sz - 1, Line(0, INF));
  }

  void update(Line &x, int k, int l, int r) {
    int mid = (l + r) >> 1;
    auto latte = x.over(seg[k], xs[l]), malta = x.over(seg[k], xs[mid]);
    if(malta) swap(seg[k], x);
    if(l + 1 >= r) return;
    else if(latte != malta) update(x, 2 * k + 1, l, mid);
    else update(x, 2 * k + 2, mid, r);
  }

  void update(T a, T b) { // ax+b
    Line l(a, b);
    update(l, 0, 0, sz);
  }

  T query(int k) { // xs[k]
    const T x = xs[k];
    k += sz - 1;
    T ret = seg[k].get(x);
    while(k > 0) {
      k = (k - 1) >> 1;
      ret = min(ret, seg[k].get(x));
    }
    return ret;
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/convex-hull-trick/li-chao-tree.cpp"
template< typename T >
struct LiChaoTree {
  struct Line {
    T a, b;

    Line(T a, T b) : a(a), b(b) {}

    inline T get(T x) const { return a * x + b; }

    inline bool over(const Line &b, const T &x) const {
      return get(x) < b.get(x);
    }
  };

  vector< T > xs;
  vector< Line > seg;
  int sz;

  LiChaoTree(const vector< T > &x, T INF) : xs(x) {
    sz = 1;
    while(sz < xs.size()) sz <<= 1;
    while(xs.size() < sz) xs.push_back(xs.back() + 1);
    seg.assign(2 * sz - 1, Line(0, INF));
  }

  void update(Line &x, int k, int l, int r) {
    int mid = (l + r) >> 1;
    auto latte = x.over(seg[k], xs[l]), malta = x.over(seg[k], xs[mid]);
    if(malta) swap(seg[k], x);
    if(l + 1 >= r) return;
    else if(latte != malta) update(x, 2 * k + 1, l, mid);
    else update(x, 2 * k + 2, mid, r);
  }

  void update(T a, T b) { // ax+b
    Line l(a, b);
    update(l, 0, 0, sz);
  }

  T query(int k) { // xs[k]
    const T x = xs[k];
    k += sz - 1;
    T ret = seg[k].get(x);
    while(k > 0) {
      k = (k - 1) >> 1;
      ret = min(ret, seg[k].get(x));
    }
    return ret;
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

