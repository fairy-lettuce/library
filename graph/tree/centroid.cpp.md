---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-2821.test.cpp
    title: test/verify/aoj-2821.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/centroid.md
    document_title: "Centroid(\u6728\u306E\u91CD\u5FC3)"
    links: []
  bundledCode: "#line 1 \"graph/tree/centroid.cpp\"\n/**\n * @brief Centroid(\u6728\
    \u306E\u91CD\u5FC3)\n * @docs docs/centroid.md\n */\ntemplate< typename T >\n\
    vector< int > centroid(const Graph< T > &g) {\n  const int N = (int) g.size();\n\
    \n  stack< pair< int, int > > st;\n  st.emplace(0, -1);\n  vector< int > sz(N),\
    \ par(N);\n  while(!st.empty()) {\n    auto p = st.top();\n    if(sz[p.first]\
    \ == 0) {\n      sz[p.first] = 1;\n      for(auto &to : g.g[p.first]) if(to !=\
    \ p.second) st.emplace(to, p.first);\n    } else {\n      for(auto &to : g.g[p.first])\
    \ if(to != p.second) sz[p.first] += sz[to];\n      par[p.first] = p.second;\n\
    \      st.pop();\n    }\n  }\n\n  vector< int > ret;\n  int size = N;\n  for(int\
    \ i = 0; i < N; i++) {\n    int val = N - sz[i];\n    for(auto &to : g.g[i]) if(to\
    \ != par[i]) val = max(val, sz[to]);\n    if(val < size) size = val, ret.clear();\n\
    \    if(val == size) ret.emplace_back(i);\n  }\n\n  return ret;\n}\n"
  code: "/**\n * @brief Centroid(\u6728\u306E\u91CD\u5FC3)\n * @docs docs/centroid.md\n\
    \ */\ntemplate< typename T >\nvector< int > centroid(const Graph< T > &g) {\n\
    \  const int N = (int) g.size();\n\n  stack< pair< int, int > > st;\n  st.emplace(0,\
    \ -1);\n  vector< int > sz(N), par(N);\n  while(!st.empty()) {\n    auto p = st.top();\n\
    \    if(sz[p.first] == 0) {\n      sz[p.first] = 1;\n      for(auto &to : g.g[p.first])\
    \ if(to != p.second) st.emplace(to, p.first);\n    } else {\n      for(auto &to\
    \ : g.g[p.first]) if(to != p.second) sz[p.first] += sz[to];\n      par[p.first]\
    \ = p.second;\n      st.pop();\n    }\n  }\n\n  vector< int > ret;\n  int size\
    \ = N;\n  for(int i = 0; i < N; i++) {\n    int val = N - sz[i];\n    for(auto\
    \ &to : g.g[i]) if(to != par[i]) val = max(val, sz[to]);\n    if(val < size) size\
    \ = val, ret.clear();\n    if(val == size) ret.emplace_back(i);\n  }\n\n  return\
    \ ret;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/tree/centroid.cpp
  requiredBy: []
  timestamp: '2020-10-26 16:42:48+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-2821.test.cpp
documentation_of: graph/tree/centroid.cpp
layout: document
redirect_from:
- /library/graph/tree/centroid.cpp
- /library/graph/tree/centroid.cpp.html
title: "Centroid(\u6728\u306E\u91CD\u5FC3)"
---
## 概要

木の重心を求める.  その頂点を取り除いたときにできる部分木たちの頂点数がすべて半分以下になる頂点を木の重心と呼び, 重心は $1$ 個か $2$ 個存在する.

* `centroid(g)`: 木 `g` の重心となる頂点をすべて返す.

## 計算量

* $O(V)$
