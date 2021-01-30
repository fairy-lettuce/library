---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    document_title: "Convert-Rooted-Tree(\u6839\u4ED8\u304D\u6728\u306B\u5909\u63DB\
      )"
    links: []
  bundledCode: "#line 1 \"graph/tree/convert-rooted-tree.cpp\"\n/**\n * @brief Convert-Rooted-Tree(\u6839\
    \u4ED8\u304D\u6728\u306B\u5909\u63DB)\n */\ntemplate< typename T >\nGraph< T >\
    \ convert_rooted_tree(const Graph< T > &g, int r = 0) {\n  int N = (int) g.size();\n\
    \  Graph< T > rg(N);\n  vector< int > v(N);\n  v[r] = 1;\n  queue< int > que;\n\
    \  que.emplace(r);\n  while(!que.empty()) {\n    auto p = que.front();\n    que.pop();\n\
    \    for(auto &to : g.g[p]) {\n      if(v[to] == 0) {\n        v[to] = 1;\n  \
    \      que.emplace(to);\n        rg.add_directed_edge(p, to, to.cost);\n     \
    \ }\n    }\n  }\n  return rg;\n}\n"
  code: "/**\n * @brief Convert-Rooted-Tree(\u6839\u4ED8\u304D\u6728\u306B\u5909\u63DB\
    )\n */\ntemplate< typename T >\nGraph< T > convert_rooted_tree(const Graph< T\
    \ > &g, int r = 0) {\n  int N = (int) g.size();\n  Graph< T > rg(N);\n  vector<\
    \ int > v(N);\n  v[r] = 1;\n  queue< int > que;\n  que.emplace(r);\n  while(!que.empty())\
    \ {\n    auto p = que.front();\n    que.pop();\n    for(auto &to : g.g[p]) {\n\
    \      if(v[to] == 0) {\n        v[to] = 1;\n        que.emplace(to);\n      \
    \  rg.add_directed_edge(p, to, to.cost);\n      }\n    }\n  }\n  return rg;\n\
    }\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/tree/convert-rooted-tree.cpp
  requiredBy: []
  timestamp: '2020-03-30 02:50:55+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: graph/tree/convert-rooted-tree.cpp
layout: document
redirect_from:
- /library/graph/tree/convert-rooted-tree.cpp
- /library/graph/tree/convert-rooted-tree.cpp.html
title: "Convert-Rooted-Tree(\u6839\u4ED8\u304D\u6728\u306B\u5909\u63DB)"
---
