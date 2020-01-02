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


# :warning: structure/bbst/randomized-binary-search-tree-lazy.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#ac1922c227762d9e573c4f7aedc86899">structure/bbst</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/bbst/randomized-binary-search-tree-lazy.cpp">View this file on GitHub</a>
    - Last commit date: 2020-01-02 23:04:20+09:00




## Code

<a id="unbundled"></a>
{% raw %}
```cpp
template< class Monoid, class OperatorMonoid = Monoid >
struct RandomizedBinarySearchTree {
  using F = function< Monoid(Monoid, Monoid) >;
  using G = function< Monoid(Monoid, OperatorMonoid) >;
  using H = function< OperatorMonoid(OperatorMonoid, OperatorMonoid) >;
  using P = function< OperatorMonoid(OperatorMonoid, int) >;

  inline int xor128() {
    static int x = 123456789;
    static int y = 362436069;
    static int z = 521288629;
    static int w = 88675123;
    int t;

    t = x ^ (x << 11);
    x = y;
    y = z;
    z = w;
    return w = (w ^ (w >> 19)) ^ (t ^ (t >> 8));
  }

  struct Node {
    Node *l, *r;
    int cnt;
    Monoid key, sum;
    OperatorMonoid lazy;

    Node() = default;

    Node(const Monoid &k, const OperatorMonoid &p) : cnt(1), key(k), sum(k), lazy(p), l(nullptr), r(nullptr) {}
  };

  vector< Node > pool;
  int ptr;

  const Monoid M1;
  const OperatorMonoid OM0;
  const F f;
  const G g;
  const H h;
  const P p;

  RandomizedBinarySearchTree(int sz, const F &f, const Monoid &M1) :
      pool(sz), ptr(0), f(f), g(G()), h(H()), p(P()), M1(M1), OM0(OperatorMonoid()) {}

  RandomizedBinarySearchTree(int sz, const F &f, const G &g, const H &h, const P &p,
                             const Monoid &M1, const OperatorMonoid &OM0) :
      pool(sz), ptr(0), f(f), g(g), h(h), p(p), M1(M1), OM0(OM0) {}

  inline Node *alloc(const Monoid &key) { return &(pool[ptr++] = Node(key, OM0)); }

  virtual Node *clone(Node *t) { return t; }

  inline int count(const Node *t) { return t ? t->cnt : 0; }

  inline Monoid sum(const Node *t) { return t ? t->sum : M1; }

  inline Node *update(Node *t) {
    t->cnt = count(t->l) + count(t->r) + 1;
    t->sum = f(f(sum(t->l), t->key), sum(t->r));
    return t;
  }

  Node *propagate(Node *t) {
    t = clone(t);
    if(t->lazy != OM0) {
      t->key = g(t->key, p(t->lazy, 1));
      if(t->l) {
        t->l = clone(t->l);
        t->l->lazy = h(t->l->lazy, t->lazy);
        t->l->sum = g(t->l->sum, p(t->lazy, count(t->l)));
      }
      if(t->r) {
        t->r = clone(t->r);
        t->r->lazy = h(t->r->lazy, t->lazy);
        t->r->sum = g(t->r->sum, p(t->lazy, count(t->r)));
      }
      t->lazy = OM0;
    }
    return update(t);
  }

  Node *merge(Node *l, Node *r) {
    if(!l || !r) return l ? l : r;
    if(xor128() % (l->cnt + r->cnt) < l->cnt) {
      l = propagate(l);
      l->r = merge(l->r, r);
      return update(l);
    } else {
      r = propagate(r);
      r->l = merge(l, r->l);
      return update(r);
    }
  }

  pair< Node *, Node * > split(Node *t, int k) {
    if(!t) return {t, t};
    t = propagate(t);
    if(k <= count(t->l)) {
      auto s = split(t->l, k);
      t->l = s.second;
      return {s.first, update(t)};
    } else {
      auto s = split(t->r, k - count(t->l) - 1);
      t->r = s.first;
      return {update(t), s.second};
    }
  }

  Node *build(int l, int r, const vector< Monoid > &v) {
    if(l + 1 >= r) return alloc(v[l]);
    return merge(build(l, (l + r) >> 1, v), build((l + r) >> 1, r, v));
  }

  Node *build(const vector< Monoid > &v) {
    ptr = 0;
    return build(0, (int) v.size(), v);
  }

  void dump(Node *r, typename vector< Monoid >::iterator &it) {
    if(!r) return;
    r = propagate(r);
    dump(r->l, it);
    *it = r->key;
    dump(r->r, ++it);
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
    for(int i = 0; i < s.size(); i++) ret += ", ";
    return (ret);
  }

  void insert(Node *&t, int k, const Monoid &v) {
    auto x = split(t, k);
    t = merge(merge(x.first, alloc(v)), x.second);
  }

  void erase(Node *&t, int k) {
    auto x = split(t, k);
    t = merge(x.first, split(x.second, 1).second);
  }

  Monoid query(Node *&t, int a, int b) {
    auto x = split(t, a);
    auto y = split(x.second, b - a);
    auto ret = sum(y.first);
    t = merge(x.first, merge(y.first, y.second));
    return ret;
  }

  void set_propagate(Node *&t, int a, int b, const OperatorMonoid &p) {
    auto x = split(t, a);
    auto y = split(x.second, b - a);
    y.first->lazy = h(y.first->lazy, p);
    t = merge(x.first, merge(propagate(y.first), y.second));
  }

  void set_element(Node *&t, int k, const Monoid &x) {
    t = propagate(t);
    if(k < count(t->l)) set_element(t->l, k, x);
    else if(k == count(t->l)) t->key = t->sum = x;
    else set_element(t->r, k - count(t->l) - 1, x);
    t = update(t);
  }


  int size(Node *t) {
    return count(t);
  }

  bool empty(Node *t) {
    return !t;
  }

  Node *makeset() {
    return nullptr;
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/bbst/randomized-binary-search-tree-lazy.cpp"
template< class Monoid, class OperatorMonoid = Monoid >
struct RandomizedBinarySearchTree {
  using F = function< Monoid(Monoid, Monoid) >;
  using G = function< Monoid(Monoid, OperatorMonoid) >;
  using H = function< OperatorMonoid(OperatorMonoid, OperatorMonoid) >;
  using P = function< OperatorMonoid(OperatorMonoid, int) >;

  inline int xor128() {
    static int x = 123456789;
    static int y = 362436069;
    static int z = 521288629;
    static int w = 88675123;
    int t;

    t = x ^ (x << 11);
    x = y;
    y = z;
    z = w;
    return w = (w ^ (w >> 19)) ^ (t ^ (t >> 8));
  }

  struct Node {
    Node *l, *r;
    int cnt;
    Monoid key, sum;
    OperatorMonoid lazy;

    Node() = default;

    Node(const Monoid &k, const OperatorMonoid &p) : cnt(1), key(k), sum(k), lazy(p), l(nullptr), r(nullptr) {}
  };

  vector< Node > pool;
  int ptr;

  const Monoid M1;
  const OperatorMonoid OM0;
  const F f;
  const G g;
  const H h;
  const P p;

  RandomizedBinarySearchTree(int sz, const F &f, const Monoid &M1) :
      pool(sz), ptr(0), f(f), g(G()), h(H()), p(P()), M1(M1), OM0(OperatorMonoid()) {}

  RandomizedBinarySearchTree(int sz, const F &f, const G &g, const H &h, const P &p,
                             const Monoid &M1, const OperatorMonoid &OM0) :
      pool(sz), ptr(0), f(f), g(g), h(h), p(p), M1(M1), OM0(OM0) {}

  inline Node *alloc(const Monoid &key) { return &(pool[ptr++] = Node(key, OM0)); }

  virtual Node *clone(Node *t) { return t; }

  inline int count(const Node *t) { return t ? t->cnt : 0; }

  inline Monoid sum(const Node *t) { return t ? t->sum : M1; }

  inline Node *update(Node *t) {
    t->cnt = count(t->l) + count(t->r) + 1;
    t->sum = f(f(sum(t->l), t->key), sum(t->r));
    return t;
  }

  Node *propagate(Node *t) {
    t = clone(t);
    if(t->lazy != OM0) {
      t->key = g(t->key, p(t->lazy, 1));
      if(t->l) {
        t->l = clone(t->l);
        t->l->lazy = h(t->l->lazy, t->lazy);
        t->l->sum = g(t->l->sum, p(t->lazy, count(t->l)));
      }
      if(t->r) {
        t->r = clone(t->r);
        t->r->lazy = h(t->r->lazy, t->lazy);
        t->r->sum = g(t->r->sum, p(t->lazy, count(t->r)));
      }
      t->lazy = OM0;
    }
    return update(t);
  }

  Node *merge(Node *l, Node *r) {
    if(!l || !r) return l ? l : r;
    if(xor128() % (l->cnt + r->cnt) < l->cnt) {
      l = propagate(l);
      l->r = merge(l->r, r);
      return update(l);
    } else {
      r = propagate(r);
      r->l = merge(l, r->l);
      return update(r);
    }
  }

  pair< Node *, Node * > split(Node *t, int k) {
    if(!t) return {t, t};
    t = propagate(t);
    if(k <= count(t->l)) {
      auto s = split(t->l, k);
      t->l = s.second;
      return {s.first, update(t)};
    } else {
      auto s = split(t->r, k - count(t->l) - 1);
      t->r = s.first;
      return {update(t), s.second};
    }
  }

  Node *build(int l, int r, const vector< Monoid > &v) {
    if(l + 1 >= r) return alloc(v[l]);
    return merge(build(l, (l + r) >> 1, v), build((l + r) >> 1, r, v));
  }

  Node *build(const vector< Monoid > &v) {
    ptr = 0;
    return build(0, (int) v.size(), v);
  }

  void dump(Node *r, typename vector< Monoid >::iterator &it) {
    if(!r) return;
    r = propagate(r);
    dump(r->l, it);
    *it = r->key;
    dump(r->r, ++it);
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
    for(int i = 0; i < s.size(); i++) ret += ", ";
    return (ret);
  }

  void insert(Node *&t, int k, const Monoid &v) {
    auto x = split(t, k);
    t = merge(merge(x.first, alloc(v)), x.second);
  }

  void erase(Node *&t, int k) {
    auto x = split(t, k);
    t = merge(x.first, split(x.second, 1).second);
  }

  Monoid query(Node *&t, int a, int b) {
    auto x = split(t, a);
    auto y = split(x.second, b - a);
    auto ret = sum(y.first);
    t = merge(x.first, merge(y.first, y.second));
    return ret;
  }

  void set_propagate(Node *&t, int a, int b, const OperatorMonoid &p) {
    auto x = split(t, a);
    auto y = split(x.second, b - a);
    y.first->lazy = h(y.first->lazy, p);
    t = merge(x.first, merge(propagate(y.first), y.second));
  }

  void set_element(Node *&t, int k, const Monoid &x) {
    t = propagate(t);
    if(k < count(t->l)) set_element(t->l, k, x);
    else if(k == count(t->l)) t->key = t->sum = x;
    else set_element(t->r, k - count(t->l) - 1, x);
    t = update(t);
  }


  int size(Node *t) {
    return count(t);
  }

  bool empty(Node *t) {
    return !t;
  }

  Node *makeset() {
    return nullptr;
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

