---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-alds-1-9-c.test.cpp
    title: test/verify/aoj-alds-1-9-c.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-k-shortest-walk.test.cpp
    title: test/verify/yosupo-k-shortest-walk.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    document_title: Leftist-Heap
    links: []
  bundledCode: "#line 1 \"structure/heap/leftist-heap.cpp\"\n/**\n * @brief Leftist-Heap\n\
    \ */\ntemplate< typename T, bool isMin = true >\nstruct LeftistHeap {\n  struct\
    \ Node {\n    Node *l, *r;\n    int s;\n    T key;\n    int idx;\n\n    explicit\
    \ Node(const T &key, int idx) : key(key), s(1), l(nullptr), r(nullptr), idx(idx)\
    \ {}\n  };\n\n  LeftistHeap() = default;\n\n  virtual Node *clone(Node *t) {\n\
    \    return t;\n  }\n\n  Node *alloc(const T &key, int idx = -1) {\n    return\
    \ new Node(key, idx);\n  }\n\n  Node *meld(Node *a, Node *b) {\n    if(!a || !b)\
    \ return a ? a : b;\n    if((a->key < b->key) ^ isMin) swap(a, b);\n    a = clone(a);\n\
    \    a->r = meld(a->r, b);\n    if(!a->l || a->l->s < a->r->s) swap(a->l, a->r);\n\
    \    a->s = (a->r ? a->r->s : 0) + 1;\n    return a;\n  }\n\n  Node *push(Node\
    \ *t, const T &key, int idx = -1) {\n    return meld(t, alloc(key, idx));\n  }\n\
    \n  Node *pop(Node *t) {\n    assert(t != nullptr);\n    return meld(t->l, t->r);\n\
    \  }\n\n  Node *make_root() {\n    return nullptr;\n  }\n};\n"
  code: "/**\n * @brief Leftist-Heap\n */\ntemplate< typename T, bool isMin = true\
    \ >\nstruct LeftistHeap {\n  struct Node {\n    Node *l, *r;\n    int s;\n   \
    \ T key;\n    int idx;\n\n    explicit Node(const T &key, int idx) : key(key),\
    \ s(1), l(nullptr), r(nullptr), idx(idx) {}\n  };\n\n  LeftistHeap() = default;\n\
    \n  virtual Node *clone(Node *t) {\n    return t;\n  }\n\n  Node *alloc(const\
    \ T &key, int idx = -1) {\n    return new Node(key, idx);\n  }\n\n  Node *meld(Node\
    \ *a, Node *b) {\n    if(!a || !b) return a ? a : b;\n    if((a->key < b->key)\
    \ ^ isMin) swap(a, b);\n    a = clone(a);\n    a->r = meld(a->r, b);\n    if(!a->l\
    \ || a->l->s < a->r->s) swap(a->l, a->r);\n    a->s = (a->r ? a->r->s : 0) + 1;\n\
    \    return a;\n  }\n\n  Node *push(Node *t, const T &key, int idx = -1) {\n \
    \   return meld(t, alloc(key, idx));\n  }\n\n  Node *pop(Node *t) {\n    assert(t\
    \ != nullptr);\n    return meld(t->l, t->r);\n  }\n\n  Node *make_root() {\n \
    \   return nullptr;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/heap/leftist-heap.cpp
  requiredBy: []
  timestamp: '2020-08-21 01:30:35+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-alds-1-9-c.test.cpp
  - test/verify/yosupo-k-shortest-walk.test.cpp
documentation_of: structure/heap/leftist-heap.cpp
layout: document
redirect_from:
- /library/structure/heap/leftist-heap.cpp
- /library/structure/heap/leftist-heap.cpp.html
title: Leftist-Heap
---
