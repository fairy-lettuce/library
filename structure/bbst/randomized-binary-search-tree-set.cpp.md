---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 1 \"structure/bbst/randomized-binary-search-tree-set.cpp\"\n\
    template< class T >\nstruct OrderedMultiSet : RandomizedBinarySearchTree< T >\n\
    {\n  using RBST = RandomizedBinarySearchTree< T >;\n  using Node = typename RBST::Node;\n\
    \n  OrderedMultiSet(int sz) : RBST(sz, [&](T x, T y) { return x; }, T()) {}\n\n\
    \  T kth_element(Node *t, int k)\n  {\n    if(k < RBST::count(t->l)) return kth_element(t->l,\
    \ k);\n    if(k == RBST::count(t->l)) return t->key;\n    return kth_element(t->r,\
    \ k - RBST::count(t->l) - 1);\n  }\n\n  virtual void insert_key(Node *&t, const\
    \ T &x)\n  {\n    RBST::insert(t, lower_bound(t, x), x);\n  }\n\n  void erase_key(Node\
    \ *&t, const T &x)\n  {\n    if(!count(t, x)) return;\n    RBST::erase(t, lower_bound(t,\
    \ x));\n  }\n\n  int count(Node *t, const T &x)\n  {\n    return upper_bound(t,\
    \ x) - lower_bound(t, x);\n  }\n\n  int lower_bound(Node *t, const T &x)\n  {\n\
    \    if(!t) return 0;\n    if(x <= t->key) return lower_bound(t->l, x);\n    return\
    \ lower_bound(t->r, x) + RBST::count(t->l) + 1;\n  }\n\n  int upper_bound(Node\
    \ *t, const T &x)\n  {\n    if(!t) return 0;\n    if(x < t->key) return upper_bound(t->l,\
    \ x);\n    return upper_bound(t->r, x) + RBST::count(t->l) + 1;\n  }\n};\ntemplate<\
    \ class T >\nstruct OrderedSet : OrderedMultiSet< T >\n{\n  using SET = OrderedMultiSet<\
    \ T >;\n  using RBST = typename SET::RBST;\n  using Node = typename RBST::Node;\n\
    \n  OrderedSet(int sz) : OrderedMultiSet< T >(sz) {}\n\n  void insert_key(Node\
    \ *&t, const T &x) override\n  {\n    if(SET::count(t, x)) return;\n    RBST::insert(t,\
    \ SET::lower_bound(t, x), x);\n  }\n};\n"
  code: "template< class T >\nstruct OrderedMultiSet : RandomizedBinarySearchTree<\
    \ T >\n{\n  using RBST = RandomizedBinarySearchTree< T >;\n  using Node = typename\
    \ RBST::Node;\n\n  OrderedMultiSet(int sz) : RBST(sz, [&](T x, T y) { return x;\
    \ }, T()) {}\n\n  T kth_element(Node *t, int k)\n  {\n    if(k < RBST::count(t->l))\
    \ return kth_element(t->l, k);\n    if(k == RBST::count(t->l)) return t->key;\n\
    \    return kth_element(t->r, k - RBST::count(t->l) - 1);\n  }\n\n  virtual void\
    \ insert_key(Node *&t, const T &x)\n  {\n    RBST::insert(t, lower_bound(t, x),\
    \ x);\n  }\n\n  void erase_key(Node *&t, const T &x)\n  {\n    if(!count(t, x))\
    \ return;\n    RBST::erase(t, lower_bound(t, x));\n  }\n\n  int count(Node *t,\
    \ const T &x)\n  {\n    return upper_bound(t, x) - lower_bound(t, x);\n  }\n\n\
    \  int lower_bound(Node *t, const T &x)\n  {\n    if(!t) return 0;\n    if(x <=\
    \ t->key) return lower_bound(t->l, x);\n    return lower_bound(t->r, x) + RBST::count(t->l)\
    \ + 1;\n  }\n\n  int upper_bound(Node *t, const T &x)\n  {\n    if(!t) return\
    \ 0;\n    if(x < t->key) return upper_bound(t->l, x);\n    return upper_bound(t->r,\
    \ x) + RBST::count(t->l) + 1;\n  }\n};\ntemplate< class T >\nstruct OrderedSet\
    \ : OrderedMultiSet< T >\n{\n  using SET = OrderedMultiSet< T >;\n  using RBST\
    \ = typename SET::RBST;\n  using Node = typename RBST::Node;\n\n  OrderedSet(int\
    \ sz) : OrderedMultiSet< T >(sz) {}\n\n  void insert_key(Node *&t, const T &x)\
    \ override\n  {\n    if(SET::count(t, x)) return;\n    RBST::insert(t, SET::lower_bound(t,\
    \ x), x);\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/bbst/randomized-binary-search-tree-set.cpp
  requiredBy: []
  timestamp: '2019-11-30 22:41:48+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: structure/bbst/randomized-binary-search-tree-set.cpp
layout: document
redirect_from:
- /library/structure/bbst/randomized-binary-search-tree-set.cpp
- /library/structure/bbst/randomized-binary-search-tree-set.cpp.html
title: structure/bbst/randomized-binary-search-tree-set.cpp
---
