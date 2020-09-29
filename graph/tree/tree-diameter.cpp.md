---
data:
  _extendedDependsOn:
  - icon: ':question:'
    path: graph/graph-template.cpp
    title: graph/graph-template.cpp
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-grl-5-a.test.cpp
    title: test/verify/aoj-grl-5-a.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-tree-diameter.test.cpp
    title: test/verify/yosupo-tree-diameter.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    document_title: "Tree-Diameter(\u6728\u306E\u76F4\u5F84)"
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
    \ Edge< T > >;\n#line 2 \"graph/tree/tree-diameter.cpp\"\n\n/**\n * @brief Tree-Diameter(\u6728\
    \u306E\u76F4\u5F84)\n */\ntemplate< typename T = int >\nstruct TreeDiameter :\
    \ Graph< T > {\npublic:\n  using Graph< T >::Graph;\n  using Graph< T >::g;\n\
    \  vector< Edge< T > > path;\n\n  T build() {\n    to.assign(g.size(), -1);\n\
    \    auto p = dfs(0, -1);\n    auto q = dfs(p.second, -1);\n\n    int now = p.second;\n\
    \    while(now != q.second) {\n      for(auto &e : g[now]) {\n        if(to[now]\
    \ == e.to) {\n          path.emplace_back(e);\n        }\n      }\n      now =\
    \ to[now];\n    }\n    return q.first;\n  }\n\n  explicit TreeDiameter(const Graph<\
    \ T > &g) : Graph< T >(g) {}\n\nprivate:\n  vector< int > to;\n\n  pair< T, int\
    \ > dfs(int idx, int par) {\n    pair< T, int > ret(0, idx);\n    for(auto &e\
    \ : g[idx]) {\n      if(e.to == par) continue;\n      auto cost = dfs(e.to, idx);\n\
    \      cost.first += e.cost;\n      if(ret < cost) {\n        ret = cost;\n  \
    \      to[idx] = e.to;\n      }\n    }\n    return ret;\n  }\n};\n"
  code: "#include \"../graph-template.cpp\"\n\n/**\n * @brief Tree-Diameter(\u6728\
    \u306E\u76F4\u5F84)\n */\ntemplate< typename T = int >\nstruct TreeDiameter :\
    \ Graph< T > {\npublic:\n  using Graph< T >::Graph;\n  using Graph< T >::g;\n\
    \  vector< Edge< T > > path;\n\n  T build() {\n    to.assign(g.size(), -1);\n\
    \    auto p = dfs(0, -1);\n    auto q = dfs(p.second, -1);\n\n    int now = p.second;\n\
    \    while(now != q.second) {\n      for(auto &e : g[now]) {\n        if(to[now]\
    \ == e.to) {\n          path.emplace_back(e);\n        }\n      }\n      now =\
    \ to[now];\n    }\n    return q.first;\n  }\n\n  explicit TreeDiameter(const Graph<\
    \ T > &g) : Graph< T >(g) {}\n\nprivate:\n  vector< int > to;\n\n  pair< T, int\
    \ > dfs(int idx, int par) {\n    pair< T, int > ret(0, idx);\n    for(auto &e\
    \ : g[idx]) {\n      if(e.to == par) continue;\n      auto cost = dfs(e.to, idx);\n\
    \      cost.first += e.cost;\n      if(ret < cost) {\n        ret = cost;\n  \
    \      to[idx] = e.to;\n      }\n    }\n    return ret;\n  }\n};\n"
  dependsOn:
  - graph/graph-template.cpp
  isVerificationFile: false
  path: graph/tree/tree-diameter.cpp
  requiredBy: []
  timestamp: '2020-09-15 01:41:10+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-tree-diameter.test.cpp
  - test/verify/aoj-grl-5-a.test.cpp
documentation_of: graph/tree/tree-diameter.cpp
layout: document
redirect_from:
- /library/graph/tree/tree-diameter.cpp
- /library/graph/tree/tree-diameter.cpp.html
title: "Tree-Diameter(\u6728\u306E\u76F4\u5F84)"
---
