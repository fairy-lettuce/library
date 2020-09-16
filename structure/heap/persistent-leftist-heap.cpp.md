---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-k-shortest-walk.test.cpp
    title: test/verify/yosupo-k-shortest-walk.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    document_title: Persistent-Leftist-Heap
    links: []
  bundledCode: "#line 1 \"structure/heap/persistent-leftist-heap.cpp\"\n/**\n * @brief\
    \ Persistent-Leftist-Heap\n */\ntemplate< typename T, bool isMin = true >\nstruct\
    \ PersistentLeftistHeap : LeftistHeap< T, isMin > {\n  using Node = typename LeftistHeap<\
    \ T, isMin >::Node;\n\n  Node *clone(Node *t) override {\n    return new Node(*t);\n\
    \  }\n};\n"
  code: "/**\n * @brief Persistent-Leftist-Heap\n */\ntemplate< typename T, bool isMin\
    \ = true >\nstruct PersistentLeftistHeap : LeftistHeap< T, isMin > {\n  using\
    \ Node = typename LeftistHeap< T, isMin >::Node;\n\n  Node *clone(Node *t) override\
    \ {\n    return new Node(*t);\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/heap/persistent-leftist-heap.cpp
  requiredBy: []
  timestamp: '2020-08-21 01:30:35+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-k-shortest-walk.test.cpp
documentation_of: structure/heap/persistent-leftist-heap.cpp
layout: document
redirect_from:
- /library/structure/heap/persistent-leftist-heap.cpp
- /library/structure/heap/persistent-leftist-heap.cpp.html
title: Persistent-Leftist-Heap
---
