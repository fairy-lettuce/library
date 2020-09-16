---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    document_title: "Persistent-Weight-Balanced-Tree(\u6C38\u7D9A\u91CD\u307F\u5E73\
      \u8861\u6728)"
    links: []
  bundledCode: "#line 1 \"structure/bbst/persistent-weight-balanced-tree.cpp\"\n/**\n\
    \ * @brief Persistent-Weight-Balanced-Tree(\u6C38\u7D9A\u91CD\u307F\u5E73\u8861\
    \u6728)\n */\ntemplate< typename Monoid, typename F, size_t FULL = 1000 >\nstruct\
    \ PersistentWeightBalancedTree : WeightBalancedTree< Monoid, F > {\n  using WBT\
    \ = WeightBalancedTree< Monoid, F >;\n  using WBT::WeightBalancedTree;\n  using\
    \ Node = typename WBT::Node;\n\nprivate:\n  Node *clone(Node *t) override {\n\
    \    return &(*WBT::pool.alloc() = *t);\n  }\n\npublic:\n  Node *rebuild(Node\
    \ *r) {\n    auto ret = WBT::dump(r);\n    WBT::pool.clear();\n    return WBT::build(ret);\n\
    \  }\n\n  bool almost_full() const {\n    return this->pool.ptr < FULL;\n  }\n\
    };\n"
  code: "/**\n * @brief Persistent-Weight-Balanced-Tree(\u6C38\u7D9A\u91CD\u307F\u5E73\
    \u8861\u6728)\n */\ntemplate< typename Monoid, typename F, size_t FULL = 1000\
    \ >\nstruct PersistentWeightBalancedTree : WeightBalancedTree< Monoid, F > {\n\
    \  using WBT = WeightBalancedTree< Monoid, F >;\n  using WBT::WeightBalancedTree;\n\
    \  using Node = typename WBT::Node;\n\nprivate:\n  Node *clone(Node *t) override\
    \ {\n    return &(*WBT::pool.alloc() = *t);\n  }\n\npublic:\n  Node *rebuild(Node\
    \ *r) {\n    auto ret = WBT::dump(r);\n    WBT::pool.clear();\n    return WBT::build(ret);\n\
    \  }\n\n  bool almost_full() const {\n    return this->pool.ptr < FULL;\n  }\n\
    };\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/bbst/persistent-weight-balanced-tree.cpp
  requiredBy: []
  timestamp: '2020-05-14 22:00:37+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: structure/bbst/persistent-weight-balanced-tree.cpp
layout: document
redirect_from:
- /library/structure/bbst/persistent-weight-balanced-tree.cpp
- /library/structure/bbst/persistent-weight-balanced-tree.cpp.html
title: "Persistent-Weight-Balanced-Tree(\u6C38\u7D9A\u91CD\u307F\u5E73\u8861\u6728\
  )"
---
