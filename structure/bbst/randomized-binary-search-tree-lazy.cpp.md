---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 1 \"structure/bbst/randomized-binary-search-tree-lazy.cpp\"\n\
    template< class Monoid, class OperatorMonoid = Monoid >\nstruct RandomizedBinarySearchTree\
    \ {\n  using F = function< Monoid(Monoid, Monoid) >;\n  using G = function< Monoid(Monoid,\
    \ OperatorMonoid) >;\n  using H = function< OperatorMonoid(OperatorMonoid, OperatorMonoid)\
    \ >;\n  using P = function< OperatorMonoid(OperatorMonoid, int) >;\n\n  inline\
    \ int xor128() {\n    static int x = 123456789;\n    static int y = 362436069;\n\
    \    static int z = 521288629;\n    static int w = 88675123;\n    int t;\n\n \
    \   t = x ^ (x << 11);\n    x = y;\n    y = z;\n    z = w;\n    return w = (w\
    \ ^ (w >> 19)) ^ (t ^ (t >> 8));\n  }\n\n  struct Node {\n    Node *l, *r;\n \
    \   int cnt;\n    Monoid key, sum;\n    OperatorMonoid lazy;\n\n    Node() = default;\n\
    \n    Node(const Monoid &k, const OperatorMonoid &p) : cnt(1), key(k), sum(k),\
    \ lazy(p), l(nullptr), r(nullptr) {}\n  };\n\n  vector< Node > pool;\n  int ptr;\n\
    \n  const Monoid M1;\n  const OperatorMonoid OM0;\n  const F f;\n  const G g;\n\
    \  const H h;\n  const P p;\n\n  RandomizedBinarySearchTree(int sz, const F &f,\
    \ const Monoid &M1) :\n      pool(sz), ptr(0), f(f), g(G()), h(H()), p(P()), M1(M1),\
    \ OM0(OperatorMonoid()) {}\n\n  RandomizedBinarySearchTree(int sz, const F &f,\
    \ const G &g, const H &h, const P &p,\n                             const Monoid\
    \ &M1, const OperatorMonoid &OM0) :\n      pool(sz), ptr(0), f(f), g(g), h(h),\
    \ p(p), M1(M1), OM0(OM0) {}\n\n  inline Node *alloc(const Monoid &key) { return\
    \ &(pool[ptr++] = Node(key, OM0)); }\n\n  virtual Node *clone(Node *t) { return\
    \ t; }\n\n  inline int count(const Node *t) { return t ? t->cnt : 0; }\n\n  inline\
    \ Monoid sum(const Node *t) { return t ? t->sum : M1; }\n\n  inline Node *update(Node\
    \ *t) {\n    t->cnt = count(t->l) + count(t->r) + 1;\n    t->sum = f(f(sum(t->l),\
    \ t->key), sum(t->r));\n    return t;\n  }\n\n  Node *propagate(Node *t) {\n \
    \   t = clone(t);\n    if(t->lazy != OM0) {\n      t->key = g(t->key, p(t->lazy,\
    \ 1));\n      if(t->l) {\n        t->l = clone(t->l);\n        t->l->lazy = h(t->l->lazy,\
    \ t->lazy);\n        t->l->sum = g(t->l->sum, p(t->lazy, count(t->l)));\n    \
    \  }\n      if(t->r) {\n        t->r = clone(t->r);\n        t->r->lazy = h(t->r->lazy,\
    \ t->lazy);\n        t->r->sum = g(t->r->sum, p(t->lazy, count(t->r)));\n    \
    \  }\n      t->lazy = OM0;\n    }\n    return update(t);\n  }\n\n  Node *merge(Node\
    \ *l, Node *r) {\n    if(!l || !r) return l ? l : r;\n    if(xor128() % (l->cnt\
    \ + r->cnt) < l->cnt) {\n      l = propagate(l);\n      l->r = merge(l->r, r);\n\
    \      return update(l);\n    } else {\n      r = propagate(r);\n      r->l =\
    \ merge(l, r->l);\n      return update(r);\n    }\n  }\n\n  pair< Node *, Node\
    \ * > split(Node *t, int k) {\n    if(!t) return {t, t};\n    t = propagate(t);\n\
    \    if(k <= count(t->l)) {\n      auto s = split(t->l, k);\n      t->l = s.second;\n\
    \      return {s.first, update(t)};\n    } else {\n      auto s = split(t->r,\
    \ k - count(t->l) - 1);\n      t->r = s.first;\n      return {update(t), s.second};\n\
    \    }\n  }\n\n  Node *build(int l, int r, const vector< Monoid > &v) {\n    if(l\
    \ + 1 >= r) return alloc(v[l]);\n    return merge(build(l, (l + r) >> 1, v), build((l\
    \ + r) >> 1, r, v));\n  }\n\n  Node *build(const vector< Monoid > &v) {\n    ptr\
    \ = 0;\n    return build(0, (int) v.size(), v);\n  }\n\n  void dump(Node *r, typename\
    \ vector< Monoid >::iterator &it) {\n    if(!r) return;\n    r = propagate(r);\n\
    \    dump(r->l, it);\n    *it = r->key;\n    dump(r->r, ++it);\n  }\n\n  vector<\
    \ Monoid > dump(Node *r) {\n    vector< Monoid > v((size_t) count(r));\n    auto\
    \ it = begin(v);\n    dump(r, it);\n    return v;\n  }\n\n  string to_string(Node\
    \ *r) {\n    auto s = dump(r);\n    string ret;\n    for(int i = 0; i < s.size();\
    \ i++) ret += \", \";\n    return (ret);\n  }\n\n  void insert(Node *&t, int k,\
    \ const Monoid &v) {\n    auto x = split(t, k);\n    t = merge(merge(x.first,\
    \ alloc(v)), x.second);\n  }\n\n  void erase(Node *&t, int k) {\n    auto x =\
    \ split(t, k);\n    t = merge(x.first, split(x.second, 1).second);\n  }\n\n  Monoid\
    \ query(Node *&t, int a, int b) {\n    auto x = split(t, a);\n    auto y = split(x.second,\
    \ b - a);\n    auto ret = sum(y.first);\n    t = merge(x.first, merge(y.first,\
    \ y.second));\n    return ret;\n  }\n\n  void set_propagate(Node *&t, int a, int\
    \ b, const OperatorMonoid &p) {\n    auto x = split(t, a);\n    auto y = split(x.second,\
    \ b - a);\n    y.first->lazy = h(y.first->lazy, p);\n    t = merge(x.first, merge(propagate(y.first),\
    \ y.second));\n  }\n\n  void set_element(Node *&t, int k, const Monoid &x) {\n\
    \    t = propagate(t);\n    if(k < count(t->l)) set_element(t->l, k, x);\n   \
    \ else if(k == count(t->l)) t->key = t->sum = x;\n    else set_element(t->r, k\
    \ - count(t->l) - 1, x);\n    t = update(t);\n  }\n\n\n  int size(Node *t) {\n\
    \    return count(t);\n  }\n\n  bool empty(Node *t) {\n    return !t;\n  }\n\n\
    \  Node *makeset() {\n    return nullptr;\n  }\n};\n"
  code: "template< class Monoid, class OperatorMonoid = Monoid >\nstruct RandomizedBinarySearchTree\
    \ {\n  using F = function< Monoid(Monoid, Monoid) >;\n  using G = function< Monoid(Monoid,\
    \ OperatorMonoid) >;\n  using H = function< OperatorMonoid(OperatorMonoid, OperatorMonoid)\
    \ >;\n  using P = function< OperatorMonoid(OperatorMonoid, int) >;\n\n  inline\
    \ int xor128() {\n    static int x = 123456789;\n    static int y = 362436069;\n\
    \    static int z = 521288629;\n    static int w = 88675123;\n    int t;\n\n \
    \   t = x ^ (x << 11);\n    x = y;\n    y = z;\n    z = w;\n    return w = (w\
    \ ^ (w >> 19)) ^ (t ^ (t >> 8));\n  }\n\n  struct Node {\n    Node *l, *r;\n \
    \   int cnt;\n    Monoid key, sum;\n    OperatorMonoid lazy;\n\n    Node() = default;\n\
    \n    Node(const Monoid &k, const OperatorMonoid &p) : cnt(1), key(k), sum(k),\
    \ lazy(p), l(nullptr), r(nullptr) {}\n  };\n\n  vector< Node > pool;\n  int ptr;\n\
    \n  const Monoid M1;\n  const OperatorMonoid OM0;\n  const F f;\n  const G g;\n\
    \  const H h;\n  const P p;\n\n  RandomizedBinarySearchTree(int sz, const F &f,\
    \ const Monoid &M1) :\n      pool(sz), ptr(0), f(f), g(G()), h(H()), p(P()), M1(M1),\
    \ OM0(OperatorMonoid()) {}\n\n  RandomizedBinarySearchTree(int sz, const F &f,\
    \ const G &g, const H &h, const P &p,\n                             const Monoid\
    \ &M1, const OperatorMonoid &OM0) :\n      pool(sz), ptr(0), f(f), g(g), h(h),\
    \ p(p), M1(M1), OM0(OM0) {}\n\n  inline Node *alloc(const Monoid &key) { return\
    \ &(pool[ptr++] = Node(key, OM0)); }\n\n  virtual Node *clone(Node *t) { return\
    \ t; }\n\n  inline int count(const Node *t) { return t ? t->cnt : 0; }\n\n  inline\
    \ Monoid sum(const Node *t) { return t ? t->sum : M1; }\n\n  inline Node *update(Node\
    \ *t) {\n    t->cnt = count(t->l) + count(t->r) + 1;\n    t->sum = f(f(sum(t->l),\
    \ t->key), sum(t->r));\n    return t;\n  }\n\n  Node *propagate(Node *t) {\n \
    \   t = clone(t);\n    if(t->lazy != OM0) {\n      t->key = g(t->key, p(t->lazy,\
    \ 1));\n      if(t->l) {\n        t->l = clone(t->l);\n        t->l->lazy = h(t->l->lazy,\
    \ t->lazy);\n        t->l->sum = g(t->l->sum, p(t->lazy, count(t->l)));\n    \
    \  }\n      if(t->r) {\n        t->r = clone(t->r);\n        t->r->lazy = h(t->r->lazy,\
    \ t->lazy);\n        t->r->sum = g(t->r->sum, p(t->lazy, count(t->r)));\n    \
    \  }\n      t->lazy = OM0;\n    }\n    return update(t);\n  }\n\n  Node *merge(Node\
    \ *l, Node *r) {\n    if(!l || !r) return l ? l : r;\n    if(xor128() % (l->cnt\
    \ + r->cnt) < l->cnt) {\n      l = propagate(l);\n      l->r = merge(l->r, r);\n\
    \      return update(l);\n    } else {\n      r = propagate(r);\n      r->l =\
    \ merge(l, r->l);\n      return update(r);\n    }\n  }\n\n  pair< Node *, Node\
    \ * > split(Node *t, int k) {\n    if(!t) return {t, t};\n    t = propagate(t);\n\
    \    if(k <= count(t->l)) {\n      auto s = split(t->l, k);\n      t->l = s.second;\n\
    \      return {s.first, update(t)};\n    } else {\n      auto s = split(t->r,\
    \ k - count(t->l) - 1);\n      t->r = s.first;\n      return {update(t), s.second};\n\
    \    }\n  }\n\n  Node *build(int l, int r, const vector< Monoid > &v) {\n    if(l\
    \ + 1 >= r) return alloc(v[l]);\n    return merge(build(l, (l + r) >> 1, v), build((l\
    \ + r) >> 1, r, v));\n  }\n\n  Node *build(const vector< Monoid > &v) {\n    ptr\
    \ = 0;\n    return build(0, (int) v.size(), v);\n  }\n\n  void dump(Node *r, typename\
    \ vector< Monoid >::iterator &it) {\n    if(!r) return;\n    r = propagate(r);\n\
    \    dump(r->l, it);\n    *it = r->key;\n    dump(r->r, ++it);\n  }\n\n  vector<\
    \ Monoid > dump(Node *r) {\n    vector< Monoid > v((size_t) count(r));\n    auto\
    \ it = begin(v);\n    dump(r, it);\n    return v;\n  }\n\n  string to_string(Node\
    \ *r) {\n    auto s = dump(r);\n    string ret;\n    for(int i = 0; i < s.size();\
    \ i++) ret += \", \";\n    return (ret);\n  }\n\n  void insert(Node *&t, int k,\
    \ const Monoid &v) {\n    auto x = split(t, k);\n    t = merge(merge(x.first,\
    \ alloc(v)), x.second);\n  }\n\n  void erase(Node *&t, int k) {\n    auto x =\
    \ split(t, k);\n    t = merge(x.first, split(x.second, 1).second);\n  }\n\n  Monoid\
    \ query(Node *&t, int a, int b) {\n    auto x = split(t, a);\n    auto y = split(x.second,\
    \ b - a);\n    auto ret = sum(y.first);\n    t = merge(x.first, merge(y.first,\
    \ y.second));\n    return ret;\n  }\n\n  void set_propagate(Node *&t, int a, int\
    \ b, const OperatorMonoid &p) {\n    auto x = split(t, a);\n    auto y = split(x.second,\
    \ b - a);\n    y.first->lazy = h(y.first->lazy, p);\n    t = merge(x.first, merge(propagate(y.first),\
    \ y.second));\n  }\n\n  void set_element(Node *&t, int k, const Monoid &x) {\n\
    \    t = propagate(t);\n    if(k < count(t->l)) set_element(t->l, k, x);\n   \
    \ else if(k == count(t->l)) t->key = t->sum = x;\n    else set_element(t->r, k\
    \ - count(t->l) - 1, x);\n    t = update(t);\n  }\n\n\n  int size(Node *t) {\n\
    \    return count(t);\n  }\n\n  bool empty(Node *t) {\n    return !t;\n  }\n\n\
    \  Node *makeset() {\n    return nullptr;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/bbst/randomized-binary-search-tree-lazy.cpp
  requiredBy: []
  timestamp: '2020-01-02 23:04:20+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: structure/bbst/randomized-binary-search-tree-lazy.cpp
layout: document
redirect_from:
- /library/structure/bbst/randomized-binary-search-tree-lazy.cpp
- /library/structure/bbst/randomized-binary-search-tree-lazy.cpp.html
title: structure/bbst/randomized-binary-search-tree-lazy.cpp
---
