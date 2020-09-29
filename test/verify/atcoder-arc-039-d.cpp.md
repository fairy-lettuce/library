---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 1 \"test/verify/atcoder-arc-039-d.cpp\"\n#define IGNORE\n\n\
    template< typename G >\nstruct DoublingLowestCommonAncestor {\n  const int LOG;\n\
    \  vector< int > dep;\n  const G &g;\n  vector< vector< int > > table;\n \n  DoublingLowestCommonAncestor(const\
    \ G &g) : g(g), dep(g.size()), LOG(32 - __builtin_clz(g.size())) {\n    table.assign(LOG,\
    \ vector< int >(g.size(), -1));\n  }\n \n  void dfs(int idx, int par, int d) {\n\
    \    table[0][idx] = par;\n    dep[idx] = d;\n    for(auto &to : g[idx]) {\n \
    \     if(to != par) dfs(to, idx, d + 1);\n    }\n  }\n \n  void build() {\n  \
    \  dfs(0, -1, 0);\n    for(int k = 0; k + 1 < LOG; k++) {\n      for(int i = 0;\
    \ i < table[k].size(); i++) {\n        if(table[k][i] == -1) table[k + 1][i] =\
    \ -1;\n        else table[k + 1][i] = table[k][table[k][i]];\n      }\n    }\n\
    \  }\n \n  int query(int u, int v) {\n    if(dep[u] > dep[v]) swap(u, v);\n  \
    \  for(int i = LOG - 1; i >= 0; i--) {\n      if(((dep[v] - dep[u]) >> i) & 1)\
    \ v = table[i][v];\n    }\n    if(u == v) return u;\n    for(int i = LOG - 1;\
    \ i >= 0; i--) {\n      if(table[i][u] != table[i][v]) {\n        u = table[i][u];\n\
    \        v = table[i][v];\n      }\n    }\n    return table[0][u];\n  }\n};\n\
    \ \nint main() {\n  int N, M;\n  scanf(\"%d %d\", &N, &M);\n  UnWeightedGraph\
    \ g(N);\n  for(int i = 0; i < M; i++) {\n    int x, y;\n    scanf(\"%d %d\", &x,\
    \ &y);\n    --x, --y;\n    g[x].emplace_back(y);\n    g[y].emplace_back(x);\n\
    \  }\n  TwoEdgeConnectedComponents< UnWeightedGraph > bcc(g);\n  UnWeightedGraph\
    \ t;\n  bcc.build(t);\n  DoublingLowestCommonAncestor< UnWeightedGraph > lca(t);\n\
    \  lca.build();\n  int Q;\n  scanf(\"%d\", &Q);\n  auto getdist = [&](int x, int\
    \ y) {\n    return lca.dep[x] + lca.dep[y] - 2 * lca.dep[lca.query(x, y)];\n \
    \ };\n  while(Q--) {\n    int a, b, c;\n    scanf(\"%d %d %d\", &a, &b, &c);\n\
    \    a = bcc[--a], b = bcc[--b], c = bcc[--c];\n    if(getdist(a, c) == getdist(a,\
    \ b) + getdist(b, c)) puts(\"OK\");\n    else puts(\"NG\");\n  }\n}\n"
  code: "#define IGNORE\n\ntemplate< typename G >\nstruct DoublingLowestCommonAncestor\
    \ {\n  const int LOG;\n  vector< int > dep;\n  const G &g;\n  vector< vector<\
    \ int > > table;\n \n  DoublingLowestCommonAncestor(const G &g) : g(g), dep(g.size()),\
    \ LOG(32 - __builtin_clz(g.size())) {\n    table.assign(LOG, vector< int >(g.size(),\
    \ -1));\n  }\n \n  void dfs(int idx, int par, int d) {\n    table[0][idx] = par;\n\
    \    dep[idx] = d;\n    for(auto &to : g[idx]) {\n      if(to != par) dfs(to,\
    \ idx, d + 1);\n    }\n  }\n \n  void build() {\n    dfs(0, -1, 0);\n    for(int\
    \ k = 0; k + 1 < LOG; k++) {\n      for(int i = 0; i < table[k].size(); i++) {\n\
    \        if(table[k][i] == -1) table[k + 1][i] = -1;\n        else table[k + 1][i]\
    \ = table[k][table[k][i]];\n      }\n    }\n  }\n \n  int query(int u, int v)\
    \ {\n    if(dep[u] > dep[v]) swap(u, v);\n    for(int i = LOG - 1; i >= 0; i--)\
    \ {\n      if(((dep[v] - dep[u]) >> i) & 1) v = table[i][v];\n    }\n    if(u\
    \ == v) return u;\n    for(int i = LOG - 1; i >= 0; i--) {\n      if(table[i][u]\
    \ != table[i][v]) {\n        u = table[i][u];\n        v = table[i][v];\n    \
    \  }\n    }\n    return table[0][u];\n  }\n};\n \nint main() {\n  int N, M;\n\
    \  scanf(\"%d %d\", &N, &M);\n  UnWeightedGraph g(N);\n  for(int i = 0; i < M;\
    \ i++) {\n    int x, y;\n    scanf(\"%d %d\", &x, &y);\n    --x, --y;\n    g[x].emplace_back(y);\n\
    \    g[y].emplace_back(x);\n  }\n  TwoEdgeConnectedComponents< UnWeightedGraph\
    \ > bcc(g);\n  UnWeightedGraph t;\n  bcc.build(t);\n  DoublingLowestCommonAncestor<\
    \ UnWeightedGraph > lca(t);\n  lca.build();\n  int Q;\n  scanf(\"%d\", &Q);\n\
    \  auto getdist = [&](int x, int y) {\n    return lca.dep[x] + lca.dep[y] - 2\
    \ * lca.dep[lca.query(x, y)];\n  };\n  while(Q--) {\n    int a, b, c;\n    scanf(\"\
    %d %d %d\", &a, &b, &c);\n    a = bcc[--a], b = bcc[--b], c = bcc[--c];\n    if(getdist(a,\
    \ c) == getdist(a, b) + getdist(b, c)) puts(\"OK\");\n    else puts(\"NG\");\n\
    \  }\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/atcoder-arc-039-d.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/atcoder-arc-039-d.cpp
layout: document
redirect_from:
- /library/test/verify/atcoder-arc-039-d.cpp
- /library/test/verify/atcoder-arc-039-d.cpp.html
title: test/verify/atcoder-arc-039-d.cpp
---
