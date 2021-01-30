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
  bundledCode: "#line 1 \"structure/bbst/persistent-red-black-tree.cpp\"\ntemplate<\
    \ typename Monoid, typename F, size_t FULL = 1000 >\nstruct PersistentRedBlackTree\
    \ : RedBlackTree< Monoid, F > {\n  using RBT = RedBlackTree< Monoid, F >;\n  using\
    \ RBT::RedBlackTree;\n  using Node = typename RBT::Node;\n\nprivate:\n  Node *clone(Node\
    \ *t) override {\n    return &(*RBT::pool.alloc() = *t);\n  }\n\npublic:\n  Node\
    \ *rebuild(Node *r) {\n    auto ret = RBT::dump(r);\n    RBT::pool.clear();\n\
    \    return RBT::build(ret);\n  }\n\n  bool almost_full() const {\n    return\
    \ this->pool.ptr < FULL;\n  }\n};\n"
  code: "template< typename Monoid, typename F, size_t FULL = 1000 >\nstruct PersistentRedBlackTree\
    \ : RedBlackTree< Monoid, F > {\n  using RBT = RedBlackTree< Monoid, F >;\n  using\
    \ RBT::RedBlackTree;\n  using Node = typename RBT::Node;\n\nprivate:\n  Node *clone(Node\
    \ *t) override {\n    return &(*RBT::pool.alloc() = *t);\n  }\n\npublic:\n  Node\
    \ *rebuild(Node *r) {\n    auto ret = RBT::dump(r);\n    RBT::pool.clear();\n\
    \    return RBT::build(ret);\n  }\n\n  bool almost_full() const {\n    return\
    \ this->pool.ptr < FULL;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/bbst/persistent-red-black-tree.cpp
  requiredBy: []
  timestamp: '2020-04-26 00:10:50+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: structure/bbst/persistent-red-black-tree.cpp
layout: document
redirect_from:
- /library/structure/bbst/persistent-red-black-tree.cpp
- /library/structure/bbst/persistent-red-black-tree.cpp.html
title: structure/bbst/persistent-red-black-tree.cpp
---
