---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    document_title: "Persistent-Lazy-Weight-Balanced-Tree(\u6C38\u7D9A\u9045\u5EF6\
      \u4F1D\u642C\u91CD\u307F\u5E73\u8861\u6728)"
    links: []
  bundledCode: "#line 1 \"structure/bbst/persistent-lazy-weight-balanced-tree.cpp\"\
    \n/**\n * @brief Persistent-Lazy-Weight-Balanced-Tree(\u6C38\u7D9A\u9045\u5EF6\
    \u4F1D\u642C\u91CD\u307F\u5E73\u8861\u6728)\n */\ntemplate< typename Monoid, typename\
    \ OperatorMonoid, typename F, typename G, typename H, size_t FULL = 1000 >\nstruct\
    \ PersistentLazyWeightBalancedTree : LazyWeightBalancedTree< Monoid, OperatorMonoid,\
    \ F, G, H > {\n  using LWBT = LazyWeightBalancedTree< Monoid, OperatorMonoid,\
    \ F, G, H >;\n  using LWBT::LazyWeightBalancedTree;\n  using Node = typename LWBT::Node;\n\
    \nprivate:\n  Node *clone(Node *t) override {\n    return &(*LWBT::pool.alloc()\
    \ = *t);\n  }\n\npublic:\n  Node *rebuild(Node *r) {\n    auto ret = LWBT::dump(r);\n\
    \    LWBT::pool.clear();\n    return LWBT::build(ret);\n  }\n\n  bool almost_full()\
    \ const {\n    return this->pool.ptr < FULL;\n  }\n};\n"
  code: "/**\n * @brief Persistent-Lazy-Weight-Balanced-Tree(\u6C38\u7D9A\u9045\u5EF6\
    \u4F1D\u642C\u91CD\u307F\u5E73\u8861\u6728)\n */\ntemplate< typename Monoid, typename\
    \ OperatorMonoid, typename F, typename G, typename H, size_t FULL = 1000 >\nstruct\
    \ PersistentLazyWeightBalancedTree : LazyWeightBalancedTree< Monoid, OperatorMonoid,\
    \ F, G, H > {\n  using LWBT = LazyWeightBalancedTree< Monoid, OperatorMonoid,\
    \ F, G, H >;\n  using LWBT::LazyWeightBalancedTree;\n  using Node = typename LWBT::Node;\n\
    \nprivate:\n  Node *clone(Node *t) override {\n    return &(*LWBT::pool.alloc()\
    \ = *t);\n  }\n\npublic:\n  Node *rebuild(Node *r) {\n    auto ret = LWBT::dump(r);\n\
    \    LWBT::pool.clear();\n    return LWBT::build(ret);\n  }\n\n  bool almost_full()\
    \ const {\n    return this->pool.ptr < FULL;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/bbst/persistent-lazy-weight-balanced-tree.cpp
  requiredBy: []
  timestamp: '2020-05-14 23:23:31+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: structure/bbst/persistent-lazy-weight-balanced-tree.cpp
layout: document
redirect_from:
- /library/structure/bbst/persistent-lazy-weight-balanced-tree.cpp
- /library/structure/bbst/persistent-lazy-weight-balanced-tree.cpp.html
title: "Persistent-Lazy-Weight-Balanced-Tree(\u6C38\u7D9A\u9045\u5EF6\u4F1D\u642C\u91CD\
  \u307F\u5E73\u8861\u6728)"
---
