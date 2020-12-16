---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-2415.test.cpp
    title: test/verify/aoj-2415.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-grl-2-b.test.cpp
    title: test/verify/aoj-grl-2-b.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links: []
  bundledCode: "#line 1 \"structure/heap/skew-heap.cpp\"\ntemplate< typename T, typename\
    \ E = T >\nstruct SkewHeap {\n  using G = function< T(T, E) >;\n  using H = function<\
    \ E(E, E) >;\n \n  struct Node {\n    T key;\n    E lazy;\n    Node *l, *r;\n\
    \  };\n \n  const bool rev;\n  const G g;\n  const H h;\n \n  SkewHeap(bool rev\
    \ = false) : g([](const T &a, const E &b) { return a + b; }),\n              \
    \                 h([](const E &a, const E &b) { return a + b; }), rev(rev) {}\n\
    \ \n  SkewHeap(const G &g, const H &h, bool rev = false) : g(g), h(h), rev(rev)\
    \ {}\n \n  Node *propagate(Node *t) {\n    if(t->lazy != 0) {\n      if(t->l)\
    \ t->l->lazy = h(t->l->lazy, t->lazy);\n      if(t->r) t->r->lazy = h(t->r->lazy,\
    \ t->lazy);\n      t->key = g(t->key, t->lazy);\n      t->lazy = 0;\n    }\n \
    \   return t;\n  }\n \n  Node *merge(Node *x, Node *y) {\n    if(!x || !y) return\
    \ x ? x : y;\n    propagate(x), propagate(y);\n    if((x->key > y->key) ^ rev)\
    \ swap(x, y);\n    x->r = merge(y, x->r);\n    swap(x->l, x->r);\n    return x;\n\
    \  }\n \n  void push(Node *&root, const T &key) {\n    root = merge(root, new\
    \ Node({key, 0, nullptr, nullptr}));\n  }\n \n  T top(Node *root) {\n    return\
    \ propagate(root)->key;\n  }\n \n  T pop(Node *&root) {\n    T top = propagate(root)->key;\n\
    \    auto *temp = root;\n    root = merge(root->l, root->r);\n    delete temp;\n\
    \    return top;\n  }\n \n  bool empty(Node *root) const {\n    return !root;\n\
    \  }\n \n  void add(Node *root, const E &lazy) {\n    if(root) {\n      root->lazy\
    \ = h(root->lazy, lazy);\n      propagate(root);\n    }\n  }\n \n  Node *makeheap()\
    \ {\n    return nullptr;\n  }\n};\n"
  code: "template< typename T, typename E = T >\nstruct SkewHeap {\n  using G = function<\
    \ T(T, E) >;\n  using H = function< E(E, E) >;\n \n  struct Node {\n    T key;\n\
    \    E lazy;\n    Node *l, *r;\n  };\n \n  const bool rev;\n  const G g;\n  const\
    \ H h;\n \n  SkewHeap(bool rev = false) : g([](const T &a, const E &b) { return\
    \ a + b; }),\n                               h([](const E &a, const E &b) { return\
    \ a + b; }), rev(rev) {}\n \n  SkewHeap(const G &g, const H &h, bool rev = false)\
    \ : g(g), h(h), rev(rev) {}\n \n  Node *propagate(Node *t) {\n    if(t->lazy !=\
    \ 0) {\n      if(t->l) t->l->lazy = h(t->l->lazy, t->lazy);\n      if(t->r) t->r->lazy\
    \ = h(t->r->lazy, t->lazy);\n      t->key = g(t->key, t->lazy);\n      t->lazy\
    \ = 0;\n    }\n    return t;\n  }\n \n  Node *merge(Node *x, Node *y) {\n    if(!x\
    \ || !y) return x ? x : y;\n    propagate(x), propagate(y);\n    if((x->key >\
    \ y->key) ^ rev) swap(x, y);\n    x->r = merge(y, x->r);\n    swap(x->l, x->r);\n\
    \    return x;\n  }\n \n  void push(Node *&root, const T &key) {\n    root = merge(root,\
    \ new Node({key, 0, nullptr, nullptr}));\n  }\n \n  T top(Node *root) {\n    return\
    \ propagate(root)->key;\n  }\n \n  T pop(Node *&root) {\n    T top = propagate(root)->key;\n\
    \    auto *temp = root;\n    root = merge(root->l, root->r);\n    delete temp;\n\
    \    return top;\n  }\n \n  bool empty(Node *root) const {\n    return !root;\n\
    \  }\n \n  void add(Node *root, const E &lazy) {\n    if(root) {\n      root->lazy\
    \ = h(root->lazy, lazy);\n      propagate(root);\n    }\n  }\n \n  Node *makeheap()\
    \ {\n    return nullptr;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/heap/skew-heap.cpp
  requiredBy: []
  timestamp: '2019-11-30 22:41:48+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-grl-2-b.test.cpp
  - test/verify/aoj-2415.test.cpp
documentation_of: structure/heap/skew-heap.cpp
layout: document
redirect_from:
- /library/structure/heap/skew-heap.cpp
- /library/structure/heap/skew-heap.cpp.html
title: structure/heap/skew-heap.cpp
---
