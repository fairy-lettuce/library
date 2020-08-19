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


# :heavy_check_mark: Dynamic-Li-Chao-Tree <small>(structure/convex-hull-trick/dynamic-li-chao-tree.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#3ad23896bbde10d07ed9c44a914e070b">structure/convex-hull-trick</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/convex-hull-trick/dynamic-li-chao-tree.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-20 03:24:24+09:00




## 概要

直線 $ax+b$ の追加クエリと, ある点 $x$ での最小値クエリを効率的に処理するデータ構造.

セグメント木の各ノードにその区間で最小の直線を載せるイメージ.

直線の追加クエリでは, そのノード $[l, r)$ の既存の直線と比較する. 交差しないとき上側の直線を捨て, 交差するときは $x$ を区間の中心 $\frac {l + r} {2}$ としたときの値の大小関係を比較する. 小さい方をそのノードの直線とし, 大きい方は子に再帰的に追加する.

点 $x$ での最小値クエリでは, $x$ を含むノードが $O(\log n)$ 個なので, それらを見ればよい.

静的な Li-Chao-Tree と動的な Li-Chao-Tree の速度差は(感覚的には)小さいため, 基本的には最小値クエリの先読みが不要な動的な方がおすすめ.

## 使い方

`x_low` には `query()` で与える $x$ の最小値, `x_high` には $x$ の最大値, `id` は単位元(十分大きい値) を指定する. すべての直線について `x_low`, `x_high` がオーバーフローしないとき意図した動作をする.

最大値クエリは最小値クエリに帰着できて, `add_line(-a, -b)`, `-query(x)` とすればよい.


* `add_line(a, b)`: 直線 $ax + b$ を追加する.
* `add_segment(l, r, a, b)`: 区間 $[l, r)$ に線分 $ax + b$ を追加する.
* `query(x)`: $ax + b$ の最小値を求める.

## 計算量

* `add_line(), query()`: $O(\log V)$
* `add_segment()`: $O(\log^2 V)$

$V$ は $x$ が動く範囲.


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-2725.test.cpp.html">test/verify/aoj-2725.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-line-add-get-min.test.cpp.html">test/verify/yosupo-line-add-get-min.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-segment-add-get-min.test.cpp.html">test/verify/yosupo-segment-add-get-min.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Dynamic-Li-Chao-Tree
 * @docs docs/dynamic-li-chao-tree.md
*/
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
/**
 * @brief Dynamic-Li-Chao-Tree
 * @docs docs/dynamic-li-chao-tree.md
*/
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

