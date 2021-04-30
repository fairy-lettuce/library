---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':x:'
    path: test/verify/yosupo-persistent-unionfind.test.cpp
    title: test/verify/yosupo-persistent-unionfind.test.cpp
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes:
    document_title: "Persistent-Union-Find(\u6C38\u7D9AUnion-Find)"
    links: []
  bundledCode: "#line 1 \"structure/union-find/persistent-union-find.cpp\"\n/*\n *\
    \ @brief Persistent-Union-Find(\u6C38\u7D9AUnion-Find)\n */\nstruct PersistentUnionFind\
    \ {\n  PersistentArray< int, 3 > data;\n\n  PersistentUnionFind() {}\n\n  PersistentUnionFind(int\
    \ sz) {\n    data.build(vector< int >(sz, -1));\n  }\n\n  int find(int k) {\n\
    \    int p = data.get(k);\n    return p >= 0 ? find(p) : k;\n  }\n\n  int size(int\
    \ k) {\n    return (-data.get(find(k)));\n  }\n\n  bool unite(int x, int y) {\n\
    \    x = find(x);\n    y = find(y);\n    if(x == y) return false;\n    auto u\
    \ = data.get(x);\n    auto v = data.get(y);\n\n    if(u < v) {\n      auto a =\
    \ data.mutable_get(x);\n      *a += v;\n      auto b = data.mutable_get(y);\n\
    \      *b = x;\n    } else {\n      auto a = data.mutable_get(y);\n      *a +=\
    \ u;\n      auto b = data.mutable_get(x);\n      *b = y;\n    }\n    return true;\n\
    \  }\n};\n"
  code: "/*\n * @brief Persistent-Union-Find(\u6C38\u7D9AUnion-Find)\n */\nstruct\
    \ PersistentUnionFind {\n  PersistentArray< int, 3 > data;\n\n  PersistentUnionFind()\
    \ {}\n\n  PersistentUnionFind(int sz) {\n    data.build(vector< int >(sz, -1));\n\
    \  }\n\n  int find(int k) {\n    int p = data.get(k);\n    return p >= 0 ? find(p)\
    \ : k;\n  }\n\n  int size(int k) {\n    return (-data.get(find(k)));\n  }\n\n\
    \  bool unite(int x, int y) {\n    x = find(x);\n    y = find(y);\n    if(x ==\
    \ y) return false;\n    auto u = data.get(x);\n    auto v = data.get(y);\n\n \
    \   if(u < v) {\n      auto a = data.mutable_get(x);\n      *a += v;\n      auto\
    \ b = data.mutable_get(y);\n      *b = x;\n    } else {\n      auto a = data.mutable_get(y);\n\
    \      *a += u;\n      auto b = data.mutable_get(x);\n      *b = y;\n    }\n \
    \   return true;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/union-find/persistent-union-find.cpp
  requiredBy: []
  timestamp: '2020-05-01 18:25:23+09:00'
  verificationStatus: LIBRARY_ALL_WA
  verifiedWith:
  - test/verify/yosupo-persistent-unionfind.test.cpp
documentation_of: structure/union-find/persistent-union-find.cpp
layout: document
redirect_from:
- /library/structure/union-find/persistent-union-find.cpp
- /library/structure/union-find/persistent-union-find.cpp.html
title: "Persistent-Union-Find(\u6C38\u7D9AUnion-Find)"
---
