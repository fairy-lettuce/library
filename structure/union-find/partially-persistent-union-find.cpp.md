---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 1 \"structure/union-find/partially-persistent-union-find.cpp\"\
    \nstruct PartiallyPersistentUnionFind {\n  vector< int > data;\n  vector< int\
    \ > last;\n  vector< vector< pair< int, int > > > add;\n\n  PartiallyPersistentUnionFind()\
    \ {}\n\n  PartiallyPersistentUnionFind(int sz) : data(sz, -1), last(sz, 1e9),\
    \ add(sz) {\n    for(auto &vs : add) vs.emplace_back(-1, -1);\n  }\n\n  bool unite(int\
    \ t, int x, int y) {\n    x = find(t, x);\n    y = find(t, y);\n    if(x == y)\
    \ return false;\n    if(data[x] > data[y]) swap(x, y);\n    data[x] += data[y];\n\
    \    add[x].emplace_back(t, data[x]);\n    data[y] = x;\n    last[y] = t;\n  \
    \  return true;\n  }\n\n  int find(int t, int x) {\n    if(t < last[x]) return\
    \ x;\n    return find(t, data[x]);\n  }\n\n  int size(int t, int x) {\n    x =\
    \ find(t, x);\n    return -prev(lower_bound(begin(add[x]), end(add[x]), make_pair(t,\
    \ 0)))->second;\n  }\n};\n"
  code: "struct PartiallyPersistentUnionFind {\n  vector< int > data;\n  vector< int\
    \ > last;\n  vector< vector< pair< int, int > > > add;\n\n  PartiallyPersistentUnionFind()\
    \ {}\n\n  PartiallyPersistentUnionFind(int sz) : data(sz, -1), last(sz, 1e9),\
    \ add(sz) {\n    for(auto &vs : add) vs.emplace_back(-1, -1);\n  }\n\n  bool unite(int\
    \ t, int x, int y) {\n    x = find(t, x);\n    y = find(t, y);\n    if(x == y)\
    \ return false;\n    if(data[x] > data[y]) swap(x, y);\n    data[x] += data[y];\n\
    \    add[x].emplace_back(t, data[x]);\n    data[y] = x;\n    last[y] = t;\n  \
    \  return true;\n  }\n\n  int find(int t, int x) {\n    if(t < last[x]) return\
    \ x;\n    return find(t, data[x]);\n  }\n\n  int size(int t, int x) {\n    x =\
    \ find(t, x);\n    return -prev(lower_bound(begin(add[x]), end(add[x]), make_pair(t,\
    \ 0)))->second;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/union-find/partially-persistent-union-find.cpp
  requiredBy: []
  timestamp: '2019-11-30 22:41:48+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: structure/union-find/partially-persistent-union-find.cpp
layout: document
redirect_from:
- /library/structure/union-find/partially-persistent-union-find.cpp
- /library/structure/union-find/partially-persistent-union-find.cpp.html
title: structure/union-find/partially-persistent-union-find.cpp
---
