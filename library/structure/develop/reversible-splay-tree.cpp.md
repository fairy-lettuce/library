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


# :heavy_check_mark: Reversible-Splay-Tree(反転可能Splay木) <small>(structure/develop/reversible-splay-tree.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#b1cd1e8cabf258d1ad55a5bb477f1b01">structure/develop</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/develop/reversible-splay-tree.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-29 03:56:51+09:00




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-2450-3.test.cpp.html">test/verify/aoj-2450-3.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-dynamic-tree-vertex-add-path-sum-2.test.cpp.html">test/verify/yosupo-dynamic-tree-vertex-add-path-sum-2.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-dynamic-tree-vertex-set-path-composite-2.test.cpp.html">test/verify/yosupo-dynamic-tree-vertex-set-path-composite-2.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-point-set-range-composite-3.test.cpp.html">test/verify/yosupo-point-set-range-composite-3.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Reversible-Splay-Tree(反転可能Splay木)
 */
template< typename Tp >
struct ReversibleSplayTreeNode {
  using T = Tp;
  ReversibleSplayTreeNode *l, *r, *p;
  T key, sum;
  bool rev;
  size_t sz;

  ReversibleSplayTreeNode() : ReversibleSplayTreeNode(Tp()) {}

  ReversibleSplayTreeNode(const T &key) :
      key(key), sum(key), rev(false), l(nullptr), r(nullptr), p(nullptr), sz(1) {}
};

template< typename Np >
struct ReversibleSplayTree : SplayTreeBase< Np > {
public:
  using Node = Np;
  using T = typename Node::T;
  using F = function< T(T, T) >;
  using S = function< T(T) >;
  using super = SplayTreeBase< Node >;

  explicit ReversibleSplayTree(const F &f, const S &s, const T &M1) :
      f(f), s(s), M1(M1) {}

  using super::splay;
  using super::split;
  using super::count;
  using super::merge;
  using super::build_node;
  using super::push_back_node;
  using super::push_front_node;
  using super::insert_node;

  inline const T &sum(const Node *t) { return t ? t->sum : M1; }

  virtual Node *alloc(const T &x) { return new Node(x); }

  T query(Node *&t, int a, int b) {
    splay(t);
    auto x = split(t, a);
    auto y = split(x.second, b - a);
    auto ret = sum(y.first);
    t = merge(x.first, y.first, y.second);
    return ret;
  }

  virtual Node *build(const vector< T > &v) {
    vector< Node * > vs(v.size());
    for(int i = 0; i < v.size(); i++) vs[i] = new Node(v[i]);
    return build_node(vs);
  }

  void toggle(Node *t) {
    swap(t->l, t->r);
    t->sum = s(t->sum);
    t->rev ^= true;
  }

  Node *update(Node *t) override {
    t->sz = 1;
    t->sum = t->key;
    if(t->l) t->sz += t->l->sz, t->sum = f(t->l->sum, t->sum);
    if(t->r) t->sz += t->r->sz, t->sum = f(t->sum, t->r->sum);
    return t;
  }

  void push(Node *t) override {
    if(t->rev) {
      if(t->l) toggle(t->l);
      if(t->r) toggle(t->r);
      t->rev = false;
    }
  }

  void set_element(Node *&t, int k, const T &x) {
    splay(t);
    sub_set_element(t, k, x);
  }

  virtual Node *push_front(Node *t, const T &x) {
    return push_front_node(t, new Node(x));
  }

  virtual Node *push_back(Node *t, const T &x) {
    return push_back_node(t, new Node(x));
  }

  virtual void insert(Node *&t, int k, const T &x) {
    insert_node(t, k, new Node(x));
  }

private:
  const T M1;
  const F f;
  const S s;

  Node *sub_set_element(Node *&t, int k, const T &x) {
    push(t);
    if(k < count(t->l)) {
      return sub_set_element(t->l, k, x);
    } else if(k == count(t->l)) {
      t->key = x;
      splay(t);
      return t;
    } else {
      return sub_set_element(t->r, k - count(t->l) - 1, x);
    }
  }
};

template< typename T >
using RST = ReversibleSplayTree< ReversibleSplayTreeNode< T > >;

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/develop/reversible-splay-tree.cpp"
/**
 * @brief Reversible-Splay-Tree(反転可能Splay木)
 */
template< typename Tp >
struct ReversibleSplayTreeNode {
  using T = Tp;
  ReversibleSplayTreeNode *l, *r, *p;
  T key, sum;
  bool rev;
  size_t sz;

  ReversibleSplayTreeNode() : ReversibleSplayTreeNode(Tp()) {}

  ReversibleSplayTreeNode(const T &key) :
      key(key), sum(key), rev(false), l(nullptr), r(nullptr), p(nullptr), sz(1) {}
};

template< typename Np >
struct ReversibleSplayTree : SplayTreeBase< Np > {
public:
  using Node = Np;
  using T = typename Node::T;
  using F = function< T(T, T) >;
  using S = function< T(T) >;
  using super = SplayTreeBase< Node >;

  explicit ReversibleSplayTree(const F &f, const S &s, const T &M1) :
      f(f), s(s), M1(M1) {}

  using super::splay;
  using super::split;
  using super::count;
  using super::merge;
  using super::build_node;
  using super::push_back_node;
  using super::push_front_node;
  using super::insert_node;

  inline const T &sum(const Node *t) { return t ? t->sum : M1; }

  virtual Node *alloc(const T &x) { return new Node(x); }

  T query(Node *&t, int a, int b) {
    splay(t);
    auto x = split(t, a);
    auto y = split(x.second, b - a);
    auto ret = sum(y.first);
    t = merge(x.first, y.first, y.second);
    return ret;
  }

  virtual Node *build(const vector< T > &v) {
    vector< Node * > vs(v.size());
    for(int i = 0; i < v.size(); i++) vs[i] = new Node(v[i]);
    return build_node(vs);
  }

  void toggle(Node *t) {
    swap(t->l, t->r);
    t->sum = s(t->sum);
    t->rev ^= true;
  }

  Node *update(Node *t) override {
    t->sz = 1;
    t->sum = t->key;
    if(t->l) t->sz += t->l->sz, t->sum = f(t->l->sum, t->sum);
    if(t->r) t->sz += t->r->sz, t->sum = f(t->sum, t->r->sum);
    return t;
  }

  void push(Node *t) override {
    if(t->rev) {
      if(t->l) toggle(t->l);
      if(t->r) toggle(t->r);
      t->rev = false;
    }
  }

  void set_element(Node *&t, int k, const T &x) {
    splay(t);
    sub_set_element(t, k, x);
  }

  virtual Node *push_front(Node *t, const T &x) {
    return push_front_node(t, new Node(x));
  }

  virtual Node *push_back(Node *t, const T &x) {
    return push_back_node(t, new Node(x));
  }

  virtual void insert(Node *&t, int k, const T &x) {
    insert_node(t, k, new Node(x));
  }

private:
  const T M1;
  const F f;
  const S s;

  Node *sub_set_element(Node *&t, int k, const T &x) {
    push(t);
    if(k < count(t->l)) {
      return sub_set_element(t->l, k, x);
    } else if(k == count(t->l)) {
      t->key = x;
      splay(t);
      return t;
    } else {
      return sub_set_element(t->r, k - count(t->l) - 1, x);
    }
  }
};

template< typename T >
using RST = ReversibleSplayTree< ReversibleSplayTreeNode< T > >;

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

