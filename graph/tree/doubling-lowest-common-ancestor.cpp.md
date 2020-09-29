---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-grl-5-c.test.cpp
    title: test/verify/aoj-grl-5-c.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    document_title: "Doubling-Lowest-Common-Ancestor(\u6700\u5C0F\u5171\u901A\u7956\
      \u5148)"
    links: []
  bundledCode: "#line 1 \"graph/tree/doubling-lowest-common-ancestor.cpp\"\n/**\n\
    \ * @brief Doubling-Lowest-Common-Ancestor(\u6700\u5C0F\u5171\u901A\u7956\u5148\
    )\n */\ntemplate< typename T >\nstruct DoublingLowestCommonAncestor : Graph< T\
    \ > {\npublic:\n  using Graph< T >::g;\n  vector< int > dep;\n  vector< T > sum;\n\
    \  vector< vector< int > > table;\n  const int LOG;\n\n  explicit DoublingLowestCommonAncestor(int\
    \ n)\n      : LOG(32 - __builtin_clz(g.size())), Graph< T >(n) {}\n\n  explicit\
    \ DoublingLowestCommonAncestor(const Graph< T > &g)\n      : LOG(32 - __builtin_clz(g.size())),\
    \ Graph< T >(g) {}\n\n  void build() {\n    dep.assign(g.size(), 0);\n    sum.assign(g.size(),\
    \ 0);\n    table.assign(LOG, vector< int >(g.size(), -1));\n    dfs(0, -1, 0);\n\
    \    for(int k = 0; k + 1 < LOG; k++) {\n      for(int i = 0; i < table[k].size();\
    \ i++) {\n        if(table[k][i] == -1) table[k + 1][i] = -1;\n        else table[k\
    \ + 1][i] = table[k][table[k][i]];\n      }\n    }\n  }\n\n  int lca(int u, int\
    \ v) {\n    if(dep[u] > dep[v]) swap(u, v);\n    for(int i = LOG - 1; i >= 0;\
    \ i--) {\n      if(((dep[v] - dep[u]) >> i) & 1) v = table[i][v];\n    }\n   \
    \ if(u == v) return u;\n    for(int i = LOG - 1; i >= 0; i--) {\n      if(table[i][u]\
    \ != table[i][v]) {\n        u = table[i][u];\n        v = table[i][v];\n    \
    \  }\n    }\n    return table[0][u];\n  }\n\n  T dist(int u, int v) {\n    return\
    \ sum[u] + sum[v] - 2 * sum[lca(u, v)];\n  }\n\nprivate:\n  void dfs(int idx,\
    \ int par, int d) {\n    table[0][idx] = par;\n    dep[idx] = d;\n    for(auto\
    \ &to : g[idx]) {\n      if(to != par) {\n        sum[to] = sum[idx] + to.cost;\n\
    \        dfs(to, idx, d + 1);\n      }\n    }\n  }\n};\n"
  code: "/**\n * @brief Doubling-Lowest-Common-Ancestor(\u6700\u5C0F\u5171\u901A\u7956\
    \u5148)\n */\ntemplate< typename T >\nstruct DoublingLowestCommonAncestor : Graph<\
    \ T > {\npublic:\n  using Graph< T >::g;\n  vector< int > dep;\n  vector< T >\
    \ sum;\n  vector< vector< int > > table;\n  const int LOG;\n\n  explicit DoublingLowestCommonAncestor(int\
    \ n)\n      : LOG(32 - __builtin_clz(g.size())), Graph< T >(n) {}\n\n  explicit\
    \ DoublingLowestCommonAncestor(const Graph< T > &g)\n      : LOG(32 - __builtin_clz(g.size())),\
    \ Graph< T >(g) {}\n\n  void build() {\n    dep.assign(g.size(), 0);\n    sum.assign(g.size(),\
    \ 0);\n    table.assign(LOG, vector< int >(g.size(), -1));\n    dfs(0, -1, 0);\n\
    \    for(int k = 0; k + 1 < LOG; k++) {\n      for(int i = 0; i < table[k].size();\
    \ i++) {\n        if(table[k][i] == -1) table[k + 1][i] = -1;\n        else table[k\
    \ + 1][i] = table[k][table[k][i]];\n      }\n    }\n  }\n\n  int lca(int u, int\
    \ v) {\n    if(dep[u] > dep[v]) swap(u, v);\n    for(int i = LOG - 1; i >= 0;\
    \ i--) {\n      if(((dep[v] - dep[u]) >> i) & 1) v = table[i][v];\n    }\n   \
    \ if(u == v) return u;\n    for(int i = LOG - 1; i >= 0; i--) {\n      if(table[i][u]\
    \ != table[i][v]) {\n        u = table[i][u];\n        v = table[i][v];\n    \
    \  }\n    }\n    return table[0][u];\n  }\n\n  T dist(int u, int v) {\n    return\
    \ sum[u] + sum[v] - 2 * sum[lca(u, v)];\n  }\n\nprivate:\n  void dfs(int idx,\
    \ int par, int d) {\n    table[0][idx] = par;\n    dep[idx] = d;\n    for(auto\
    \ &to : g[idx]) {\n      if(to != par) {\n        sum[to] = sum[idx] + to.cost;\n\
    \        dfs(to, idx, d + 1);\n      }\n    }\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/tree/doubling-lowest-common-ancestor.cpp
  requiredBy: []
  timestamp: '2020-03-26 01:02:16+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-grl-5-c.test.cpp
documentation_of: graph/tree/doubling-lowest-common-ancestor.cpp
layout: document
redirect_from:
- /library/graph/tree/doubling-lowest-common-ancestor.cpp
- /library/graph/tree/doubling-lowest-common-ancestor.cpp.html
title: "Doubling-Lowest-Common-Ancestor(\u6700\u5C0F\u5171\u901A\u7956\u5148)"
---
