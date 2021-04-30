---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-2450-3.test.cpp
    title: test/verify/aoj-2450-3.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-dynamic-tree-vertex-add-path-sum-2.test.cpp
    title: test/verify/yosupo-dynamic-tree-vertex-add-path-sum-2.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-dynamic-tree-vertex-set-path-composite-2.test.cpp
    title: test/verify/yosupo-dynamic-tree-vertex-set-path-composite-2.test.cpp
  - icon: ':x:'
    path: test/verify/yosupo-point-set-range-composite-3.test.cpp
    title: test/verify/yosupo-point-set-range-composite-3.test.cpp
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':question:'
  attributes:
    document_title: "Reversible-Splay-Tree(\u53CD\u8EE2\u53EF\u80FDSplay\u6728)"
    links: []
  bundledCode: "#line 1 \"structure/develop/reversible-splay-tree.cpp\"\n/**\n * @brief\
    \ Reversible-Splay-Tree(\u53CD\u8EE2\u53EF\u80FDSplay\u6728)\n */\ntemplate< typename\
    \ Tp >\nstruct ReversibleSplayTreeNode {\n  using T = Tp;\n  ReversibleSplayTreeNode\
    \ *l, *r, *p;\n  T key, sum;\n  bool rev;\n  size_t sz;\n\n  ReversibleSplayTreeNode()\
    \ : ReversibleSplayTreeNode(Tp()) {}\n\n  ReversibleSplayTreeNode(const T &key)\
    \ :\n      key(key), sum(key), rev(false), l(nullptr), r(nullptr), p(nullptr),\
    \ sz(1) {}\n};\n\ntemplate< typename Np >\nstruct ReversibleSplayTree : SplayTreeBase<\
    \ Np > {\npublic:\n  using Node = Np;\n  using T = typename Node::T;\n  using\
    \ F = function< T(T, T) >;\n  using S = function< T(T) >;\n  using super = SplayTreeBase<\
    \ Node >;\n\n  explicit ReversibleSplayTree(const F &f, const S &s, const T &M1)\
    \ :\n      f(f), s(s), M1(M1) {}\n\n  using super::splay;\n  using super::split;\n\
    \  using super::count;\n  using super::merge;\n  using super::build_node;\n  using\
    \ super::push_back_node;\n  using super::push_front_node;\n  using super::insert_node;\n\
    \n  inline const T &sum(const Node *t) { return t ? t->sum : M1; }\n\n  virtual\
    \ Node *alloc(const T &x) { return new Node(x); }\n\n  T query(Node *&t, int a,\
    \ int b) {\n    splay(t);\n    auto x = split(t, a);\n    auto y = split(x.second,\
    \ b - a);\n    auto ret = sum(y.first);\n    t = merge(x.first, y.first, y.second);\n\
    \    return ret;\n  }\n\n  virtual Node *build(const vector< T > &v) {\n    vector<\
    \ Node * > vs(v.size());\n    for(int i = 0; i < v.size(); i++) vs[i] = new Node(v[i]);\n\
    \    return build_node(vs);\n  }\n\n  void toggle(Node *t) {\n    swap(t->l, t->r);\n\
    \    t->sum = s(t->sum);\n    t->rev ^= true;\n  }\n\n  Node *update(Node *t)\
    \ override {\n    t->sz = 1;\n    t->sum = t->key;\n    if(t->l) t->sz += t->l->sz,\
    \ t->sum = f(t->l->sum, t->sum);\n    if(t->r) t->sz += t->r->sz, t->sum = f(t->sum,\
    \ t->r->sum);\n    return t;\n  }\n\n  void push(Node *t) override {\n    if(t->rev)\
    \ {\n      if(t->l) toggle(t->l);\n      if(t->r) toggle(t->r);\n      t->rev\
    \ = false;\n    }\n  }\n\n  void set_element(Node *&t, int k, const T &x) {\n\
    \    splay(t);\n    sub_set_element(t, k, x);\n  }\n\n  virtual Node *push_front(Node\
    \ *t, const T &x) {\n    return push_front_node(t, new Node(x));\n  }\n\n  virtual\
    \ Node *push_back(Node *t, const T &x) {\n    return push_back_node(t, new Node(x));\n\
    \  }\n\n  virtual void insert(Node *&t, int k, const T &x) {\n    insert_node(t,\
    \ k, new Node(x));\n  }\n\nprivate:\n  const T M1;\n  const F f;\n  const S s;\n\
    \n  Node *sub_set_element(Node *&t, int k, const T &x) {\n    push(t);\n    if(k\
    \ < count(t->l)) {\n      return sub_set_element(t->l, k, x);\n    } else if(k\
    \ == count(t->l)) {\n      t->key = x;\n      splay(t);\n      return t;\n   \
    \ } else {\n      return sub_set_element(t->r, k - count(t->l) - 1, x);\n    }\n\
    \  }\n};\n\ntemplate< typename T >\nusing RST = ReversibleSplayTree< ReversibleSplayTreeNode<\
    \ T > >;\n"
  code: "/**\n * @brief Reversible-Splay-Tree(\u53CD\u8EE2\u53EF\u80FDSplay\u6728\
    )\n */\ntemplate< typename Tp >\nstruct ReversibleSplayTreeNode {\n  using T =\
    \ Tp;\n  ReversibleSplayTreeNode *l, *r, *p;\n  T key, sum;\n  bool rev;\n  size_t\
    \ sz;\n\n  ReversibleSplayTreeNode() : ReversibleSplayTreeNode(Tp()) {}\n\n  ReversibleSplayTreeNode(const\
    \ T &key) :\n      key(key), sum(key), rev(false), l(nullptr), r(nullptr), p(nullptr),\
    \ sz(1) {}\n};\n\ntemplate< typename Np >\nstruct ReversibleSplayTree : SplayTreeBase<\
    \ Np > {\npublic:\n  using Node = Np;\n  using T = typename Node::T;\n  using\
    \ F = function< T(T, T) >;\n  using S = function< T(T) >;\n  using super = SplayTreeBase<\
    \ Node >;\n\n  explicit ReversibleSplayTree(const F &f, const S &s, const T &M1)\
    \ :\n      f(f), s(s), M1(M1) {}\n\n  using super::splay;\n  using super::split;\n\
    \  using super::count;\n  using super::merge;\n  using super::build_node;\n  using\
    \ super::push_back_node;\n  using super::push_front_node;\n  using super::insert_node;\n\
    \n  inline const T &sum(const Node *t) { return t ? t->sum : M1; }\n\n  virtual\
    \ Node *alloc(const T &x) { return new Node(x); }\n\n  T query(Node *&t, int a,\
    \ int b) {\n    splay(t);\n    auto x = split(t, a);\n    auto y = split(x.second,\
    \ b - a);\n    auto ret = sum(y.first);\n    t = merge(x.first, y.first, y.second);\n\
    \    return ret;\n  }\n\n  virtual Node *build(const vector< T > &v) {\n    vector<\
    \ Node * > vs(v.size());\n    for(int i = 0; i < v.size(); i++) vs[i] = new Node(v[i]);\n\
    \    return build_node(vs);\n  }\n\n  void toggle(Node *t) {\n    swap(t->l, t->r);\n\
    \    t->sum = s(t->sum);\n    t->rev ^= true;\n  }\n\n  Node *update(Node *t)\
    \ override {\n    t->sz = 1;\n    t->sum = t->key;\n    if(t->l) t->sz += t->l->sz,\
    \ t->sum = f(t->l->sum, t->sum);\n    if(t->r) t->sz += t->r->sz, t->sum = f(t->sum,\
    \ t->r->sum);\n    return t;\n  }\n\n  void push(Node *t) override {\n    if(t->rev)\
    \ {\n      if(t->l) toggle(t->l);\n      if(t->r) toggle(t->r);\n      t->rev\
    \ = false;\n    }\n  }\n\n  void set_element(Node *&t, int k, const T &x) {\n\
    \    splay(t);\n    sub_set_element(t, k, x);\n  }\n\n  virtual Node *push_front(Node\
    \ *t, const T &x) {\n    return push_front_node(t, new Node(x));\n  }\n\n  virtual\
    \ Node *push_back(Node *t, const T &x) {\n    return push_back_node(t, new Node(x));\n\
    \  }\n\n  virtual void insert(Node *&t, int k, const T &x) {\n    insert_node(t,\
    \ k, new Node(x));\n  }\n\nprivate:\n  const T M1;\n  const F f;\n  const S s;\n\
    \n  Node *sub_set_element(Node *&t, int k, const T &x) {\n    push(t);\n    if(k\
    \ < count(t->l)) {\n      return sub_set_element(t->l, k, x);\n    } else if(k\
    \ == count(t->l)) {\n      t->key = x;\n      splay(t);\n      return t;\n   \
    \ } else {\n      return sub_set_element(t->r, k - count(t->l) - 1, x);\n    }\n\
    \  }\n};\n\ntemplate< typename T >\nusing RST = ReversibleSplayTree< ReversibleSplayTreeNode<\
    \ T > >;\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/develop/reversible-splay-tree.cpp
  requiredBy: []
  timestamp: '2020-08-29 03:56:51+09:00'
  verificationStatus: LIBRARY_SOME_WA
  verifiedWith:
  - test/verify/aoj-2450-3.test.cpp
  - test/verify/yosupo-dynamic-tree-vertex-add-path-sum-2.test.cpp
  - test/verify/yosupo-point-set-range-composite-3.test.cpp
  - test/verify/yosupo-dynamic-tree-vertex-set-path-composite-2.test.cpp
documentation_of: structure/develop/reversible-splay-tree.cpp
layout: document
redirect_from:
- /library/structure/develop/reversible-splay-tree.cpp
- /library/structure/develop/reversible-splay-tree.cpp.html
title: "Reversible-Splay-Tree(\u53CD\u8EE2\u53EF\u80FDSplay\u6728)"
---
