---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':x:'
    path: test/verify/aoj-2450-3.test.cpp
    title: test/verify/aoj-2450-3.test.cpp
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes:
    document_title: "Lazy-Reversible-Splay-Tree(\u9045\u5EF6\u4F1D\u642C\u53CD\u8EE2\
      \u53EF\u80FDSplay\u6728)"
    links: []
  bundledCode: "#line 1 \"structure/develop/lazy-reversible-splay-tree.cpp\"\n/**\n\
    \ * @brief Lazy-Reversible-Splay-Tree(\u9045\u5EF6\u4F1D\u642C\u53CD\u8EE2\u53EF\
    \u80FDSplay\u6728)\n */\ntemplate< typename Tp, typename Ep >\nstruct LazyReversibleSplayTreeNode\
    \ {\n  using T = Tp;\n  using E = Ep;\n  LazyReversibleSplayTreeNode *l, *r, *p;\n\
    \  T key, sum;\n  E lazy;\n  bool rev;\n  size_t sz;\n\n  LazyReversibleSplayTreeNode()\
    \ : LazyReversibleSplayTreeNode(Tp()) {}\n\n  LazyReversibleSplayTreeNode(const\
    \ T &key) :\n      LazyReversibleSplayTreeNode(key, E()) {}\n\n  LazyReversibleSplayTreeNode(const\
    \ T &key, const E &lazy) :\n      key(key), sum(key), rev(false), l(nullptr),\
    \ r(nullptr), p(nullptr), sz(1), lazy(lazy) {}\n};\n\ntemplate< typename Np >\n\
    struct LazyReversibleSplayTree : ReversibleSplayTree< Np > {\npublic:\npublic:\n\
    \  using Node = Np;\n  using T = typename Node::T;\n  using E = typename Node::E;\n\
    \  using super = ReversibleSplayTree< Node >;\n  using F = typename super::F;\n\
    \  using G = function< T(T, E) >;\n  using H = function< E(E, E) >;\n  using S\
    \ = typename super::S;\n  using NP = typename super::NP;\n\n  explicit LazyReversibleSplayTree(const\
    \ F &f, const G &g, const H &h, const S &s,\n                                \
    \   const T &M1, const E &OM0) :\n      g(g), h(h), OM0(OM0), super(f, s, M1)\
    \ {}\n\n\n  using super::splay;\n  using super::split;\n  using super::count;\n\
    \  using super::merge;\n  using super::build_node;\n  using super::toggle;\n \
    \ using super::insert_node;\n\n  NP alloc(const T &x) override { return new Node(x,\
    \ OM0); }\n\n  void push(NP t) override {\n    if(t->lazy != OM0) {\n      if(t->l)\
    \ propagate(t->l, t->lazy);\n      if(t->r) propagate(t->r, t->lazy);\n      t->lazy\
    \ = OM0;\n    }\n    super::push(t);\n  }\n\n  NP set_propagate(NP& t, int a,\
    \ int b, const E &pp) {\n    splay(t);\n    auto x = split(t, a);\n    auto y\
    \ = split(x.second, b - a);\n    set_propagate(y.first, pp);\n    return t = merge(x.first,\
    \ y.first, y.second);\n  }\n\n  void set_propagate(NP t, const E &pp) {\n    splay(t);\n\
    \    propagate(t, pp);\n    push(t);\n  }\n\nprivate:\n  const E OM0;\n  const\
    \ G g;\n  const H h;\n\n  void propagate(NP t, const E &x) {\n    t->lazy = h(t->lazy,\
    \ x);\n    t->key = g(t->key, x);\n    t->sum = g(t->sum, x);\n  }\n};\n\ntemplate<\
    \ typename T, typename E >\nusing LRST = LazyReversibleSplayTree< LazyReversibleSplayTreeNode<\
    \ T, E > >;\n"
  code: "/**\n * @brief Lazy-Reversible-Splay-Tree(\u9045\u5EF6\u4F1D\u642C\u53CD\u8EE2\
    \u53EF\u80FDSplay\u6728)\n */\ntemplate< typename Tp, typename Ep >\nstruct LazyReversibleSplayTreeNode\
    \ {\n  using T = Tp;\n  using E = Ep;\n  LazyReversibleSplayTreeNode *l, *r, *p;\n\
    \  T key, sum;\n  E lazy;\n  bool rev;\n  size_t sz;\n\n  LazyReversibleSplayTreeNode()\
    \ : LazyReversibleSplayTreeNode(Tp()) {}\n\n  LazyReversibleSplayTreeNode(const\
    \ T &key) :\n      LazyReversibleSplayTreeNode(key, E()) {}\n\n  LazyReversibleSplayTreeNode(const\
    \ T &key, const E &lazy) :\n      key(key), sum(key), rev(false), l(nullptr),\
    \ r(nullptr), p(nullptr), sz(1), lazy(lazy) {}\n};\n\ntemplate< typename Np >\n\
    struct LazyReversibleSplayTree : ReversibleSplayTree< Np > {\npublic:\npublic:\n\
    \  using Node = Np;\n  using T = typename Node::T;\n  using E = typename Node::E;\n\
    \  using super = ReversibleSplayTree< Node >;\n  using F = typename super::F;\n\
    \  using G = function< T(T, E) >;\n  using H = function< E(E, E) >;\n  using S\
    \ = typename super::S;\n  using NP = typename super::NP;\n\n  explicit LazyReversibleSplayTree(const\
    \ F &f, const G &g, const H &h, const S &s,\n                                \
    \   const T &M1, const E &OM0) :\n      g(g), h(h), OM0(OM0), super(f, s, M1)\
    \ {}\n\n\n  using super::splay;\n  using super::split;\n  using super::count;\n\
    \  using super::merge;\n  using super::build_node;\n  using super::toggle;\n \
    \ using super::insert_node;\n\n  NP alloc(const T &x) override { return new Node(x,\
    \ OM0); }\n\n  void push(NP t) override {\n    if(t->lazy != OM0) {\n      if(t->l)\
    \ propagate(t->l, t->lazy);\n      if(t->r) propagate(t->r, t->lazy);\n      t->lazy\
    \ = OM0;\n    }\n    super::push(t);\n  }\n\n  NP set_propagate(NP& t, int a,\
    \ int b, const E &pp) {\n    splay(t);\n    auto x = split(t, a);\n    auto y\
    \ = split(x.second, b - a);\n    set_propagate(y.first, pp);\n    return t = merge(x.first,\
    \ y.first, y.second);\n  }\n\n  void set_propagate(NP t, const E &pp) {\n    splay(t);\n\
    \    propagate(t, pp);\n    push(t);\n  }\n\nprivate:\n  const E OM0;\n  const\
    \ G g;\n  const H h;\n\n  void propagate(NP t, const E &x) {\n    t->lazy = h(t->lazy,\
    \ x);\n    t->key = g(t->key, x);\n    t->sum = g(t->sum, x);\n  }\n};\n\ntemplate<\
    \ typename T, typename E >\nusing LRST = LazyReversibleSplayTree< LazyReversibleSplayTreeNode<\
    \ T, E > >;\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/develop/lazy-reversible-splay-tree.cpp
  requiredBy: []
  timestamp: '2021-05-08 18:25:40+09:00'
  verificationStatus: LIBRARY_ALL_WA
  verifiedWith:
  - test/verify/aoj-2450-3.test.cpp
documentation_of: structure/develop/lazy-reversible-splay-tree.cpp
layout: document
redirect_from:
- /library/structure/develop/lazy-reversible-splay-tree.cpp
- /library/structure/develop/lazy-reversible-splay-tree.cpp.html
title: "Lazy-Reversible-Splay-Tree(\u9045\u5EF6\u4F1D\u642C\u53CD\u8EE2\u53EF\u80FD\
  Splay\u6728)"
---
