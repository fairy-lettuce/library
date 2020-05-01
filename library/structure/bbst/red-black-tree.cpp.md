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


# :heavy_check_mark: Red-Black-Tree(赤黒木) <small>(structure/bbst/red-black-tree.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#ac1922c227762d9e573c4f7aedc86899">structure/bbst</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/bbst/red-black-tree.cpp">View this file on GitHub</a>
    - Last commit date: 2020-05-01 18:08:24+09:00




## 概要

Red-Black-Tree は平衡二分探索木の一種. RBSTとは異なり葉にデータをもたせる実装(葉木)なので, pool の大きさを $2$ 倍とる必要がある.

merge-split ベースによる実装.

* `RedBlackTree(n, f, M1)`: サイズ `n` で初期化する. ここで `f` は2つの区間の要素をマージする二項演算, `M1` はモノイドの単位元である.
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
* `push_front(t, v)`: 木 `t` の先頭にノード `v` を挿入する.
* `push_back(t, v)`: 木 `t` の末尾にノード `v` を挿入する.
* `pop_front(t)`: 木 `t` の先頭要素を削除する.
* `pop_back(t)`: 木 `t` の末尾要素を削除する.

## 計算量

* $O(\log n)$ 但し `build` と `dump` は $O(n)$


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-1508-2.test.cpp.html">test/verify/aoj-1508-2.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-staticrmq-3.test.cpp.html">test/verify/yosupo-staticrmq-3.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Red-Black-Tree(赤黒木)
 * @docs docs/red-black-tree.md
 */
template< typename Monoid, typename F >
struct RedBlackTree {
public:
  enum COLOR {
    BLACK, RED
  };

  struct Node {
    Node *l, *r;
    COLOR color;
    int level, cnt;
    Monoid key, sum;

    Node() {}

    Node(const Monoid &k) :
        key(k), sum(k), l(nullptr), r(nullptr), color(BLACK), level(0), cnt(1) {}

    Node(Node *l, Node *r, const Monoid &k) :
        key(k), color(RED), l(l), r(r) {}

    bool is_leaf() const {
      return l == nullptr;
    }
  };

private:
  inline Node *alloc(Node *l, Node *r) {
    auto t = &(*pool.alloc() = Node(l, r, M1));
    return update(t);
  }

  virtual Node *clone(Node *t) {
    return t;
  }

  Node *rotate(Node *t, bool b) {
    t = clone(t);
    Node *s;
    if(b) {
      s = clone(t->l);
      t->l = s->r;
      s->r = t;
    } else {
      s = clone(t->r);
      t->r = s->l;
      s->l = t;
    }
    update(t);
    return update(s);
  }

  Node *submerge(Node *l, Node *r) {
    if(l->level < r->level) {
      r = clone(r);
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
      l = clone(l);
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
    t->cnt = count(t->l) + count(t->r) + (!t->l || !t->r);
    t->level = t->l ? t->l->level + (t->l->color == BLACK) : 0;
    t->sum = f(f(sum(t->l), t->key), sum(t->r));
    return t;
  }

  void dump(Node *r, typename vector< Monoid >::iterator &it) {
    if(r->is_leaf()) {
      *it++ = r->key;
      return;
    }
    dump(r->l, it);
    dump(r->r, it);
  }

  Node *merge(Node *l) {
    return l;
  }

public:

  VectorPool< Node > pool;
  const F f;
  const Monoid M1;

  RedBlackTree(int sz, const F &f, const Monoid &M1) :
      pool(sz), M1(M1), f(f) { pool.clear(); }


  inline Node *alloc(const Monoid &key) {
    return &(*pool.alloc() = Node(key));
  }

  inline int count(const Node *t) { return t ? t->cnt : 0; }

  inline const Monoid &sum(const Node *t) { return t ? t->sum : M1; }

  pair< Node *, Node * > split(Node *t, int k) {
    if(!t) return {nullptr, nullptr};
    if(k == 0) return {nullptr, t};
    if(k >= count(t)) return {t, nullptr};
    t = clone(t);
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
    dump(r, it);
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
    auto ret = sum(y.first);
    t = merge(x.first, merge(y.first, y.second));
    return ret;
  }

  void set_element(Node *&t, int k, const Monoid &x) {
    t = clone(t);
    if(t->is_leaf()) {
      t->key = t->sum = x;
      return;
    }
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
#line 1 "structure/bbst/red-black-tree.cpp"
/**
 * @brief Red-Black-Tree(赤黒木)
 * @docs docs/red-black-tree.md
 */
template< typename Monoid, typename F >
struct RedBlackTree {
public:
  enum COLOR {
    BLACK, RED
  };

  struct Node {
    Node *l, *r;
    COLOR color;
    int level, cnt;
    Monoid key, sum;

    Node() {}

    Node(const Monoid &k) :
        key(k), sum(k), l(nullptr), r(nullptr), color(BLACK), level(0), cnt(1) {}

    Node(Node *l, Node *r, const Monoid &k) :
        key(k), color(RED), l(l), r(r) {}

    bool is_leaf() const {
      return l == nullptr;
    }
  };

private:
  inline Node *alloc(Node *l, Node *r) {
    auto t = &(*pool.alloc() = Node(l, r, M1));
    return update(t);
  }

  virtual Node *clone(Node *t) {
    return t;
  }

  Node *rotate(Node *t, bool b) {
    t = clone(t);
    Node *s;
    if(b) {
      s = clone(t->l);
      t->l = s->r;
      s->r = t;
    } else {
      s = clone(t->r);
      t->r = s->l;
      s->l = t;
    }
    update(t);
    return update(s);
  }

  Node *submerge(Node *l, Node *r) {
    if(l->level < r->level) {
      r = clone(r);
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
      l = clone(l);
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
    t->cnt = count(t->l) + count(t->r) + (!t->l || !t->r);
    t->level = t->l ? t->l->level + (t->l->color == BLACK) : 0;
    t->sum = f(f(sum(t->l), t->key), sum(t->r));
    return t;
  }

  void dump(Node *r, typename vector< Monoid >::iterator &it) {
    if(r->is_leaf()) {
      *it++ = r->key;
      return;
    }
    dump(r->l, it);
    dump(r->r, it);
  }

  Node *merge(Node *l) {
    return l;
  }

public:

  VectorPool< Node > pool;
  const F f;
  const Monoid M1;

  RedBlackTree(int sz, const F &f, const Monoid &M1) :
      pool(sz), M1(M1), f(f) { pool.clear(); }


  inline Node *alloc(const Monoid &key) {
    return &(*pool.alloc() = Node(key));
  }

  inline int count(const Node *t) { return t ? t->cnt : 0; }

  inline const Monoid &sum(const Node *t) { return t ? t->sum : M1; }

  pair< Node *, Node * > split(Node *t, int k) {
    if(!t) return {nullptr, nullptr};
    if(k == 0) return {nullptr, t};
    if(k >= count(t)) return {t, nullptr};
    t = clone(t);
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
    dump(r, it);
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
    auto ret = sum(y.first);
    t = merge(x.first, merge(y.first, y.second));
    return ret;
  }

  void set_element(Node *&t, int k, const Monoid &x) {
    t = clone(t);
    if(t->is_leaf()) {
      t->key = t->sum = x;
      return;
    }
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

