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


# :heavy_check_mark: Lazy-Red-Black-Tree(遅延伝搬赤黒木) <small>(structure/bbst/lazy-red-black-tree.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#ac1922c227762d9e573c4f7aedc86899">structure/bbst</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/bbst/lazy-red-black-tree.cpp">View this file on GitHub</a>
    - Last commit date: 2020-05-01 18:16:03+09:00




## 概要

Lazy-Red-Black-Tree は Red-Black-Tree に遅延伝搬を実装したものである.

* `LazyRedBlackTree(n, f, g, h, M1, OM0)`: サイズ `n` で初期化する. ここで `f` は2つの区間の要素をマージする二項演算, `g` は要素と作用素をマージする二項演算, `h` は作用素同士をマージする二項演算, `M1` はモノイドの単位元, `OM0` は作用素の単位元である.
* `split(t, k)`: 木 `t` を $[0, k)[k, n)$ で分割する.
* `split3(t, a, b)`: 木 `t` を $[0, a)[a, b)[b, n)$ で分割する.
* `merge(l, r)`: 木 `l` と木 `r` を併合する.
* `build(v)`: 配列 `v` をもとに木を構築する.
* `dump(r)`: 木 `r` の葉を通りがけ順に格納したものを返す.
* `to_string(r)`: `dump(r)` をスペース区切りで文字列として連結したものを返す.
* `insert(t, k, v)`: 木 `t` の位置 `k` (0-indexed) にノード `v` を挿入する.
* `erase(t, k)`: 木 `t` の位置 `k` (0-indexed) のノードを削除する.
* `query(t, l, r)`: 区間 $[l, r)$ の要素を二項演算した結果を返す.
* `set_element(t, k, x)`: 木 `t` の位置 `k` (0-indexed) のノードを `x` に変更する.
* `set_propagate(t, a, b, pp)`: 木 `t` の区間 $[a, b)$ の要素に作用素 `pp` を適用する.
* `push_front(t, v)`: 木 `t` の先頭にノード `v` を挿入する.
* `push_back(t, v)`: 木 `t` の末尾にノード `v` を挿入する.
* `pop_front(t)`: 木 `t` の先頭要素を削除する.
* `pop_back(t)`: 木 `t` の末尾要素を削除する.

## 計算量

* $O(\log n)$ 但し `build` と `dump` は $O(n)$


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-range-affine-range-sum-2.test.cpp.html">test/verify/yosupo-range-affine-range-sum-2.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Lazy-Red-Black-Tree(遅延伝搬赤黒木)
 * @docs docs/lazy-red-black-tree.md
 */
template< typename Monoid, typename OperatorMonoid, typename F, typename G, typename H >
struct LazyRedBlackTree {
public:
  enum COLOR {
    BLACK, RED
  };

  struct Node {
    Node *l, *r;
    COLOR color;
    int level, cnt;
    Monoid key, sum;
    OperatorMonoid lazy;

    Node() {}

    Node(const Monoid &k, const OperatorMonoid &laz) :
        key(k), sum(k), l(nullptr), r(nullptr), color(BLACK), level(0), cnt(1), lazy(laz) {}

    Node(Node *l, Node *r, const Monoid &k, const OperatorMonoid &laz) :
        key(k), color(RED), l(l), r(r), lazy(laz) {}

    bool is_leaf() const {
      return l == nullptr;
    }
  };

private:
  Node *propagate(Node *t) {
    t = clone(t);
    if(t->lazy != OM0) {
      if(t->is_leaf()) {
        t->key = g(t->key, t->lazy);
      } else {
        if(t->l) {
          t->l = clone(t->l);
          t->l->lazy = h(t->l->lazy, t->lazy);
          t->l->sum = g(t->l->sum, t->lazy);
        }
        if(t->r) {
          t->r = clone(t->r);
          t->r->lazy = h(t->r->lazy, t->lazy);
          t->r->sum = g(t->r->sum, t->lazy);
        }
      }
      t->lazy = OM0;
    }
    return update(t);
  }

  inline Node *alloc(Node *l, Node *r) {
    auto t = &(*pool.alloc() = Node(l, r, M1, OM0));
    return update(t);
  }

  virtual Node *clone(Node *t) {
    return t;
  }

  Node *rotate(Node *t, bool b) {
    t = propagate(t);
    Node *s;
    if(b) {
      s = propagate(t->l);
      t->l = s->r;
      s->r = t;
    } else {
      s = propagate(t->r);
      t->r = s->l;
      s->l = t;
    }
    update(t);
    return update(s);
  }

  Node *submerge(Node *l, Node *r) {
    if(l->level < r->level) {
      r = propagate(r);
      Node *c = (r->l = submerge(l, r->l));
      if(r->color == BLACK && c->color == RED && c->l && c->l->color == RED) {
        r->color = RED;
        c->color = BLACK;
        if(r->r->color == BLACK) return rotate(r, true);
        r->r->color = BLACK;
      }
      return update(r);
    }
    if(l->level > r->level) {
      l = propagate(l);
      Node *c = (l->r = submerge(l->r, r));
      if(l->color == BLACK && c->color == RED && c->r && c->r->color == RED) {
        l->color = RED;
        c->color = BLACK;
        if(l->l->color == BLACK) return rotate(l, false);
        l->l->color = BLACK;
      }
      return update(l);
    }
    return alloc(l, r);
  }

  Node *build(int l, int r, const vector< Monoid > &v) {
    if(l + 1 >= r) return alloc(v[l]);
    return merge(build(l, (l + r) >> 1, v), build((l + r) >> 1, r, v));
  }

  Node *update(Node *t) {
    t->cnt = count(t->l) + count(t->r) + t->is_leaf();
    t->level = t->is_leaf() ? 0 : t->l->level + (t->l->color == BLACK);
    t->sum = f(f(sum(t->l), t->key), sum(t->r));
    return t;
  }

  void dump(Node *r, typename vector< Monoid >::iterator &it, OperatorMonoid lazy) {
    if(r->lazy != OM0) lazy = h(lazy, r->lazy);
    if(r->is_leaf()) {
      *it++ = g(r->key, lazy);
      return;
    }
    dump(r->l, it, lazy);
    dump(r->r, it, lazy);
  }

  Node *merge(Node *l) {
    return l;
  }

public:

  VectorPool< Node > pool;
  const F f;
  const G g;
  const H h;
  const OperatorMonoid OM0;
  const Monoid M1;

  LazyRedBlackTree(int sz, const F &f, const G &g, const H &h, const Monoid &M1, const OperatorMonoid &OM0) :
      pool(sz), M1(M1), OM0(OM0), f(f), g(g), h(h) { pool.clear(); }


  inline Node *alloc(const Monoid &key) {
    return &(*pool.alloc() = Node(key, OM0));
  }

  inline int count(const Node *t) { return t ? t->cnt : 0; }

  inline const Monoid &sum(const Node *t) { return t ? t->sum : M1; }

  pair< Node *, Node * > split(Node *t, int k) {
    if(!t) return {nullptr, nullptr};
    t = propagate(t);
    if(k == 0) return {nullptr, t};
    if(k >= count(t)) return {t, nullptr};
    Node *l = t->l, *r = t->r;
    pool.free(t);
    if(k < count(l)) {
      auto pp = split(l, k);
      return {pp.first, merge(pp.second, r)};
    }
    if(k > count(l)) {
      auto pp = split(r, k - count(l));
      return {merge(l, pp.first), pp.second};
    }
    return {l, r};
  }

  tuple< Node *, Node *, Node * > split3(Node *t, int a, int b) {
    auto x = split(t, a);
    auto y = split(x.second, b - a);
    return make_tuple(x.first, y.first, y.second);
  }

  template< typename ... Args >
  Node *merge(Node *l, Args ...rest) {
    Node *r = merge(rest...);
    if(!l || !r) return l ? l : r;
    Node *c = submerge(l, r);
    c->color = BLACK;
    return c;
  }

  Node *build(const vector< Monoid > &v) {
    return build(0, (int) v.size(), v);
  }

  vector< Monoid > dump(Node *r) {
    vector< Monoid > v((size_t) count(r));
    auto it = begin(v);
    dump(r, it, OM0);
    return v;
  }

  string to_string(Node *r) {
    auto s = dump(r);
    string ret;
    for(int i = 0; i < s.size(); i++) {
      ret += std::to_string(s[i]);
      ret += ", ";
    }
    return ret;
  }

  void insert(Node *&t, int k, const Monoid &v) {
    auto x = split(t, k);
    t = merge(merge(x.first, alloc(v)), x.second);
  }

  Monoid erase(Node *&t, int k) {
    auto x = split(t, k);
    auto y = split(x.second, 1);
    auto v = y.first->key;
    pool.free(y.first);
    t = merge(x.first, y.second);
    return v;
  }

  Monoid query(Node *&t, int a, int b) {
    auto x = split(t, a);
    auto y = split(x.second, b - a);
    Monoid ret = sum(y.first);
    t = merge(x.first, y.first, y.second);
    return ret;
  }

  void set_propagate(Node *&t, int a, int b, const OperatorMonoid &pp) {
    auto x = split(t, a);
    auto y = split(x.second, b - a);
    y.first->lazy = h(y.first->lazy, pp);
    t = merge(x.first, propagate(y.first), y.second);
  }

  void set_element(Node *&t, int k, const Monoid &x) {
    if(t->is_leaf()) {
      t->key = t->sum = x;
      return;
    }
    t = propagate(t);
    if(k < count(t->l)) set_element(t->l, k, x);
    else set_element(t->r, k - count(t->l), x);
    t = update(t);
  }

  void push_front(Node *&t, const Monoid &v) {
    t = merge(alloc(v), t);
  }

  void push_back(Node *&t, const Monoid &v) {
    t = merge(t, alloc(v));
  }

  Monoid pop_front(Node *&t) {
    auto ret = split(t, 1);
    t = ret.second;
    return ret.first->key;
  }

  Monoid pop_back(Node *&t) {
    auto ret = split(t, count(t) - 1);
    t = ret.first;
    return ret.second->key;
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/bbst/lazy-red-black-tree.cpp"
/**
 * @brief Lazy-Red-Black-Tree(遅延伝搬赤黒木)
 * @docs docs/lazy-red-black-tree.md
 */
template< typename Monoid, typename OperatorMonoid, typename F, typename G, typename H >
struct LazyRedBlackTree {
public:
  enum COLOR {
    BLACK, RED
  };

  struct Node {
    Node *l, *r;
    COLOR color;
    int level, cnt;
    Monoid key, sum;
    OperatorMonoid lazy;

    Node() {}

    Node(const Monoid &k, const OperatorMonoid &laz) :
        key(k), sum(k), l(nullptr), r(nullptr), color(BLACK), level(0), cnt(1), lazy(laz) {}

    Node(Node *l, Node *r, const Monoid &k, const OperatorMonoid &laz) :
        key(k), color(RED), l(l), r(r), lazy(laz) {}

    bool is_leaf() const {
      return l == nullptr;
    }
  };

private:
  Node *propagate(Node *t) {
    t = clone(t);
    if(t->lazy != OM0) {
      if(t->is_leaf()) {
        t->key = g(t->key, t->lazy);
      } else {
        if(t->l) {
          t->l = clone(t->l);
          t->l->lazy = h(t->l->lazy, t->lazy);
          t->l->sum = g(t->l->sum, t->lazy);
        }
        if(t->r) {
          t->r = clone(t->r);
          t->r->lazy = h(t->r->lazy, t->lazy);
          t->r->sum = g(t->r->sum, t->lazy);
        }
      }
      t->lazy = OM0;
    }
    return update(t);
  }

  inline Node *alloc(Node *l, Node *r) {
    auto t = &(*pool.alloc() = Node(l, r, M1, OM0));
    return update(t);
  }

  virtual Node *clone(Node *t) {
    return t;
  }

  Node *rotate(Node *t, bool b) {
    t = propagate(t);
    Node *s;
    if(b) {
      s = propagate(t->l);
      t->l = s->r;
      s->r = t;
    } else {
      s = propagate(t->r);
      t->r = s->l;
      s->l = t;
    }
    update(t);
    return update(s);
  }

  Node *submerge(Node *l, Node *r) {
    if(l->level < r->level) {
      r = propagate(r);
      Node *c = (r->l = submerge(l, r->l));
      if(r->color == BLACK && c->color == RED && c->l && c->l->color == RED) {
        r->color = RED;
        c->color = BLACK;
        if(r->r->color == BLACK) return rotate(r, true);
        r->r->color = BLACK;
      }
      return update(r);
    }
    if(l->level > r->level) {
      l = propagate(l);
      Node *c = (l->r = submerge(l->r, r));
      if(l->color == BLACK && c->color == RED && c->r && c->r->color == RED) {
        l->color = RED;
        c->color = BLACK;
        if(l->l->color == BLACK) return rotate(l, false);
        l->l->color = BLACK;
      }
      return update(l);
    }
    return alloc(l, r);
  }

  Node *build(int l, int r, const vector< Monoid > &v) {
    if(l + 1 >= r) return alloc(v[l]);
    return merge(build(l, (l + r) >> 1, v), build((l + r) >> 1, r, v));
  }

  Node *update(Node *t) {
    t->cnt = count(t->l) + count(t->r) + t->is_leaf();
    t->level = t->is_leaf() ? 0 : t->l->level + (t->l->color == BLACK);
    t->sum = f(f(sum(t->l), t->key), sum(t->r));
    return t;
  }

  void dump(Node *r, typename vector< Monoid >::iterator &it, OperatorMonoid lazy) {
    if(r->lazy != OM0) lazy = h(lazy, r->lazy);
    if(r->is_leaf()) {
      *it++ = g(r->key, lazy);
      return;
    }
    dump(r->l, it, lazy);
    dump(r->r, it, lazy);
  }

  Node *merge(Node *l) {
    return l;
  }

public:

  VectorPool< Node > pool;
  const F f;
  const G g;
  const H h;
  const OperatorMonoid OM0;
  const Monoid M1;

  LazyRedBlackTree(int sz, const F &f, const G &g, const H &h, const Monoid &M1, const OperatorMonoid &OM0) :
      pool(sz), M1(M1), OM0(OM0), f(f), g(g), h(h) { pool.clear(); }


  inline Node *alloc(const Monoid &key) {
    return &(*pool.alloc() = Node(key, OM0));
  }

  inline int count(const Node *t) { return t ? t->cnt : 0; }

  inline const Monoid &sum(const Node *t) { return t ? t->sum : M1; }

  pair< Node *, Node * > split(Node *t, int k) {
    if(!t) return {nullptr, nullptr};
    t = propagate(t);
    if(k == 0) return {nullptr, t};
    if(k >= count(t)) return {t, nullptr};
    Node *l = t->l, *r = t->r;
    pool.free(t);
    if(k < count(l)) {
      auto pp = split(l, k);
      return {pp.first, merge(pp.second, r)};
    }
    if(k > count(l)) {
      auto pp = split(r, k - count(l));
      return {merge(l, pp.first), pp.second};
    }
    return {l, r};
  }

  tuple< Node *, Node *, Node * > split3(Node *t, int a, int b) {
    auto x = split(t, a);
    auto y = split(x.second, b - a);
    return make_tuple(x.first, y.first, y.second);
  }

  template< typename ... Args >
  Node *merge(Node *l, Args ...rest) {
    Node *r = merge(rest...);
    if(!l || !r) return l ? l : r;
    Node *c = submerge(l, r);
    c->color = BLACK;
    return c;
  }

  Node *build(const vector< Monoid > &v) {
    return build(0, (int) v.size(), v);
  }

  vector< Monoid > dump(Node *r) {
    vector< Monoid > v((size_t) count(r));
    auto it = begin(v);
    dump(r, it, OM0);
    return v;
  }

  string to_string(Node *r) {
    auto s = dump(r);
    string ret;
    for(int i = 0; i < s.size(); i++) {
      ret += std::to_string(s[i]);
      ret += ", ";
    }
    return ret;
  }

  void insert(Node *&t, int k, const Monoid &v) {
    auto x = split(t, k);
    t = merge(merge(x.first, alloc(v)), x.second);
  }

  Monoid erase(Node *&t, int k) {
    auto x = split(t, k);
    auto y = split(x.second, 1);
    auto v = y.first->key;
    pool.free(y.first);
    t = merge(x.first, y.second);
    return v;
  }

  Monoid query(Node *&t, int a, int b) {
    auto x = split(t, a);
    auto y = split(x.second, b - a);
    Monoid ret = sum(y.first);
    t = merge(x.first, y.first, y.second);
    return ret;
  }

  void set_propagate(Node *&t, int a, int b, const OperatorMonoid &pp) {
    auto x = split(t, a);
    auto y = split(x.second, b - a);
    y.first->lazy = h(y.first->lazy, pp);
    t = merge(x.first, propagate(y.first), y.second);
  }

  void set_element(Node *&t, int k, const Monoid &x) {
    if(t->is_leaf()) {
      t->key = t->sum = x;
      return;
    }
    t = propagate(t);
    if(k < count(t->l)) set_element(t->l, k, x);
    else set_element(t->r, k - count(t->l), x);
    t = update(t);
  }

  void push_front(Node *&t, const Monoid &v) {
    t = merge(alloc(v), t);
  }

  void push_back(Node *&t, const Monoid &v) {
    t = merge(t, alloc(v));
  }

  Monoid pop_front(Node *&t) {
    auto ret = split(t, 1);
    t = ret.second;
    return ret.first->key;
  }

  Monoid pop_back(Node *&t) {
    auto ret = split(t, count(t) - 1);
    t = ret.first;
    return ret.second->key;
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

