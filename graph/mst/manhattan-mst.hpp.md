---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':x:'
    path: test/verify/yosupo-manhattanmst.test.cpp
    title: test/verify/yosupo-manhattanmst.test.cpp
  _isVerificationFailed: true
  _pathExtension: hpp
  _verificationStatusIcon: ':x:'
  attributes:
    document_title: Manhattan MST
    links: []
  bundledCode: "#line 1 \"graph/mst/manhattan-mst.hpp\"\n/**\n * @brief Manhattan\
    \ MST\n */\ntemplate< typename T >\nEdges< T > manhattan_mst(vector< T > xs, vector<\
    \ T > ys) {\n  assert(xs.size() == ys.size());\n  Edges< T > ret;\n  int n = (int)\
    \ xs.size();\n\n  vector< int > ord(n);\n  iota(ord.begin(), ord.end(), 0);\n\n\
    \  for(int s = 0; s < 2; s++) {\n    for(int t = 0; t < 2; t++) {\n      auto\
    \ cmp = [&](int i, int j) -> bool {\n        return xs[i] + ys[i] < xs[j] + ys[j];\n\
    \      };\n      sort(ord.begin(), ord.end(), cmp);\n\n      map< T, int > idx;\n\
    \      for(int i:ord) {\n        for(auto it = idx.lower_bound(-ys[i]);\n    \
    \        it != idx.end(); it = idx.erase(it)) {\n          int j = it->second;\n\
    \          if(xs[i] - xs[j] < ys[i] - ys[j]) break;\n          ret.emplace_back(i,\
    \ j, abs(xs[i] - xs[j]) + abs(ys[i] - ys[j]));\n        }\n        idx[-ys[i]]\
    \ = i;\n      }\n      swap(xs, ys);\n    }\n    for(int i = 0; i < n; i++) xs[i]\
    \ *= -1;\n  }\n  return ret;\n}\n"
  code: "/**\n * @brief Manhattan MST\n */\ntemplate< typename T >\nEdges< T > manhattan_mst(vector<\
    \ T > xs, vector< T > ys) {\n  assert(xs.size() == ys.size());\n  Edges< T > ret;\n\
    \  int n = (int) xs.size();\n\n  vector< int > ord(n);\n  iota(ord.begin(), ord.end(),\
    \ 0);\n\n  for(int s = 0; s < 2; s++) {\n    for(int t = 0; t < 2; t++) {\n  \
    \    auto cmp = [&](int i, int j) -> bool {\n        return xs[i] + ys[i] < xs[j]\
    \ + ys[j];\n      };\n      sort(ord.begin(), ord.end(), cmp);\n\n      map< T,\
    \ int > idx;\n      for(int i:ord) {\n        for(auto it = idx.lower_bound(-ys[i]);\n\
    \            it != idx.end(); it = idx.erase(it)) {\n          int j = it->second;\n\
    \          if(xs[i] - xs[j] < ys[i] - ys[j]) break;\n          ret.emplace_back(i,\
    \ j, abs(xs[i] - xs[j]) + abs(ys[i] - ys[j]));\n        }\n        idx[-ys[i]]\
    \ = i;\n      }\n      swap(xs, ys);\n    }\n    for(int i = 0; i < n; i++) xs[i]\
    \ *= -1;\n  }\n  return ret;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/mst/manhattan-mst.hpp
  requiredBy: []
  timestamp: '2021-08-16 02:34:50+09:00'
  verificationStatus: LIBRARY_ALL_WA
  verifiedWith:
  - test/verify/yosupo-manhattanmst.test.cpp
documentation_of: graph/mst/manhattan-mst.hpp
layout: document
redirect_from:
- /library/graph/mst/manhattan-mst.hpp
- /library/graph/mst/manhattan-mst.hpp.html
title: Manhattan MST
---
