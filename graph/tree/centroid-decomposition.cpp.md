---
data:
  _extendedDependsOn:
  - icon: ':x:'
    path: graph/graph-template.cpp
    title: graph/graph-template.cpp
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':x:'
    path: test/verify/aoj-3139.test.cpp
    title: test/verify/aoj-3139.test.cpp
  - icon: ':x:'
    path: test/verify/yosupo-frequency-table-of-tree-distance.test.cpp
    title: test/verify/yosupo-frequency-table-of-tree-distance.test.cpp
  - icon: ':x:'
    path: test/verify/yukicoder-1002.test.cpp
    title: test/verify/yukicoder-1002.test.cpp
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes:
    document_title: "Centroid-Decomosition(\u91CD\u5FC3\u5206\u89E3)"
    links: []
  bundledCode: "#line 2 \"graph/graph-template.cpp\"\n\ntemplate< typename T = int\
    \ >\nstruct Edge {\n  int from, to;\n  T cost;\n  int idx;\n\n  Edge() = default;\n\
    \n  Edge(int from, int to, T cost = 1, int idx = -1) : from(from), to(to), cost(cost),\
    \ idx(idx) {}\n\n  operator int() const { return to; }\n};\n\ntemplate< typename\
    \ T = int >\nstruct Graph {\n  vector< vector< Edge< T > > > g;\n  int es;\n\n\
    \  Graph() = default;\n\n  explicit Graph(int n) : g(n), es(0) {}\n\n  size_t\
    \ size() const {\n    return g.size();\n  }\n\n  void add_directed_edge(int from,\
    \ int to, T cost = 1) {\n    g[from].emplace_back(from, to, cost, es++);\n  }\n\
    \n  void add_edge(int from, int to, T cost = 1) {\n    g[from].emplace_back(from,\
    \ to, cost, es);\n    g[to].emplace_back(to, from, cost, es++);\n  }\n\n  void\
    \ read(int M, int padding = -1, bool weighted = false, bool directed = false)\
    \ {\n    for(int i = 0; i < M; i++) {\n      int a, b;\n      cin >> a >> b;\n\
    \      a += padding;\n      b += padding;\n      T c = T(1);\n      if(weighted)\
    \ cin >> c;\n      if(directed) add_directed_edge(a, b, c);\n      else add_edge(a,\
    \ b, c);\n    }\n  }\n};\n\ntemplate< typename T = int >\nusing Edges = vector<\
    \ Edge< T > >;\n#line 2 \"graph/tree/centroid-decomposition.cpp\"\n\n/**\n * @brief\
    \ Centroid-Decomosition(\u91CD\u5FC3\u5206\u89E3)\n */\ntemplate< typename T >\n\
    struct CentroidDecomposition : Graph< T > {\npublic:\n  using Graph< T >::Graph;\n\
    \  using Graph< T >::g;\n  Graph< int > tree;\n\n  int build(int t = 0) {\n  \
    \  sub.assign(g.size(), 0);\n    v.assign(g.size(), 0);\n    tree = Graph< T >(g.size());\n\
    \    return build_dfs(0);\n  }\n\n  explicit CentroidDecomposition(const Graph<\
    \ T > &g) : Graph< T >(g) {}\n\nprivate:\n  vector< int > sub;\n  vector< int\
    \ > v;\n\n  inline int build_dfs(int idx, int par) {\n    sub[idx] = 1;\n    for(auto\
    \ &to : g[idx]) {\n      if(to == par || v[to]) continue;\n      sub[idx] += build_dfs(to,\
    \ idx);\n    }\n    return sub[idx];\n  }\n\n  inline int search_centroid(int\
    \ idx, int par, const int mid) {\n    for(auto &to : g[idx]) {\n      if(to ==\
    \ par || v[to]) continue;\n      if(sub[to] > mid) return search_centroid(to,\
    \ idx, mid);\n    }\n    return idx;\n  }\n\n  inline int build_dfs(int idx) {\n\
    \    int centroid = search_centroid(idx, -1, build_dfs(idx, -1) / 2);\n    v[centroid]\
    \ = true;\n    for(auto &to : g[centroid]) {\n      if(!v[to]) tree.add_directed_edge(centroid,\
    \ build_dfs(to));\n    }\n    v[centroid] = false;\n    return centroid;\n  }\n\
    };\n"
  code: "#include \"../graph-template.cpp\"\n\n/**\n * @brief Centroid-Decomosition(\u91CD\
    \u5FC3\u5206\u89E3)\n */\ntemplate< typename T >\nstruct CentroidDecomposition\
    \ : Graph< T > {\npublic:\n  using Graph< T >::Graph;\n  using Graph< T >::g;\n\
    \  Graph< int > tree;\n\n  int build(int t = 0) {\n    sub.assign(g.size(), 0);\n\
    \    v.assign(g.size(), 0);\n    tree = Graph< T >(g.size());\n    return build_dfs(0);\n\
    \  }\n\n  explicit CentroidDecomposition(const Graph< T > &g) : Graph< T >(g)\
    \ {}\n\nprivate:\n  vector< int > sub;\n  vector< int > v;\n\n  inline int build_dfs(int\
    \ idx, int par) {\n    sub[idx] = 1;\n    for(auto &to : g[idx]) {\n      if(to\
    \ == par || v[to]) continue;\n      sub[idx] += build_dfs(to, idx);\n    }\n \
    \   return sub[idx];\n  }\n\n  inline int search_centroid(int idx, int par, const\
    \ int mid) {\n    for(auto &to : g[idx]) {\n      if(to == par || v[to]) continue;\n\
    \      if(sub[to] > mid) return search_centroid(to, idx, mid);\n    }\n    return\
    \ idx;\n  }\n\n  inline int build_dfs(int idx) {\n    int centroid = search_centroid(idx,\
    \ -1, build_dfs(idx, -1) / 2);\n    v[centroid] = true;\n    for(auto &to : g[centroid])\
    \ {\n      if(!v[to]) tree.add_directed_edge(centroid, build_dfs(to));\n    }\n\
    \    v[centroid] = false;\n    return centroid;\n  }\n};\n"
  dependsOn:
  - graph/graph-template.cpp
  isVerificationFile: false
  path: graph/tree/centroid-decomposition.cpp
  requiredBy: []
  timestamp: '2020-09-15 01:04:53+09:00'
  verificationStatus: LIBRARY_ALL_WA
  verifiedWith:
  - test/verify/yosupo-frequency-table-of-tree-distance.test.cpp
  - test/verify/yukicoder-1002.test.cpp
  - test/verify/aoj-3139.test.cpp
documentation_of: graph/tree/centroid-decomposition.cpp
layout: document
redirect_from:
- /library/graph/tree/centroid-decomposition.cpp
- /library/graph/tree/centroid-decomposition.cpp.html
title: "Centroid-Decomosition(\u91CD\u5FC3\u5206\u89E3)"
---
