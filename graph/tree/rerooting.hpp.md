---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-1595.test.cpp
    title: test/verify/aoj-1595.test.cpp
  _isVerificationFailed: false
  _pathExtension: hpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links: []
  bundledCode: "#line 1 \"graph/tree/rerooting.hpp\"\ntemplate< typename sum_t, typename\
    \ key_t >\nstruct ReRooting {\n  struct Edge {\n    int to;\n    key_t data;\n\
    \    sum_t dp, ndp;\n  };\n\n  using F = function< sum_t(sum_t, sum_t) >;\n  using\
    \ G = function< sum_t(sum_t, key_t) >;\n\n  vector< vector< Edge > > g;\n  const\
    \ F f;\n  const G gg;\n  const sum_t ident;\n  vector< sum_t > subdp, dp;\n\n\
    \  ReRooting(int V, const F f, const G g, const sum_t &ident)\n      : g(V), f(f),\
    \ gg(g), ident(ident), subdp(V, ident), dp(V, ident) {}\n\n  void add_edge(int\
    \ u, int v, const key_t &d) {\n    g[u].emplace_back((Edge) {v, d, ident, ident});\n\
    \    g[v].emplace_back((Edge) {u, d, ident, ident});\n  }\n\n  void add_edge_bi(int\
    \ u, int v, const key_t &d, const key_t &e) {\n    g[u].emplace_back((Edge) {v,\
    \ d, ident, ident});\n    g[v].emplace_back((Edge) {u, e, ident, ident});\n  }\n\
    \n  void dfs_sub(int idx, int par) {\n    for(auto &e : g[idx]) {\n      if(e.to\
    \ == par) continue;\n      dfs_sub(e.to, idx);\n      subdp[idx] = f(subdp[idx],\
    \ gg(subdp[e.to], e.data));\n    }\n  }\n\n  void dfs_all(int idx, int par, const\
    \ sum_t &top) {\n    sum_t buff{ident};\n    for(int i = 0; i < (int) g[idx].size();\
    \ i++) {\n      auto &e = g[idx][i];\n      e.ndp = buff;\n      e.dp = gg(par\
    \ == e.to ? top : subdp[e.to], e.data);\n      buff = f(buff, e.dp);\n    }\n\
    \    dp[idx] = buff;\n    buff = ident;\n    for(int i = (int) g[idx].size() -\
    \ 1; i >= 0; i--) {\n      auto &e = g[idx][i];\n      if(e.to != par) dfs_all(e.to,\
    \ idx, f(e.ndp, buff));\n      e.ndp = f(e.ndp, buff);\n      buff = f(buff, e.dp);\n\
    \    }\n  }\n\n  vector< sum_t > build() {\n    dfs_sub(0, -1);\n    dfs_all(0,\
    \ -1, ident);\n    return dp;\n  }\n};\n"
  code: "template< typename sum_t, typename key_t >\nstruct ReRooting {\n  struct\
    \ Edge {\n    int to;\n    key_t data;\n    sum_t dp, ndp;\n  };\n\n  using F\
    \ = function< sum_t(sum_t, sum_t) >;\n  using G = function< sum_t(sum_t, key_t)\
    \ >;\n\n  vector< vector< Edge > > g;\n  const F f;\n  const G gg;\n  const sum_t\
    \ ident;\n  vector< sum_t > subdp, dp;\n\n  ReRooting(int V, const F f, const\
    \ G g, const sum_t &ident)\n      : g(V), f(f), gg(g), ident(ident), subdp(V,\
    \ ident), dp(V, ident) {}\n\n  void add_edge(int u, int v, const key_t &d) {\n\
    \    g[u].emplace_back((Edge) {v, d, ident, ident});\n    g[v].emplace_back((Edge)\
    \ {u, d, ident, ident});\n  }\n\n  void add_edge_bi(int u, int v, const key_t\
    \ &d, const key_t &e) {\n    g[u].emplace_back((Edge) {v, d, ident, ident});\n\
    \    g[v].emplace_back((Edge) {u, e, ident, ident});\n  }\n\n  void dfs_sub(int\
    \ idx, int par) {\n    for(auto &e : g[idx]) {\n      if(e.to == par) continue;\n\
    \      dfs_sub(e.to, idx);\n      subdp[idx] = f(subdp[idx], gg(subdp[e.to], e.data));\n\
    \    }\n  }\n\n  void dfs_all(int idx, int par, const sum_t &top) {\n    sum_t\
    \ buff{ident};\n    for(int i = 0; i < (int) g[idx].size(); i++) {\n      auto\
    \ &e = g[idx][i];\n      e.ndp = buff;\n      e.dp = gg(par == e.to ? top : subdp[e.to],\
    \ e.data);\n      buff = f(buff, e.dp);\n    }\n    dp[idx] = buff;\n    buff\
    \ = ident;\n    for(int i = (int) g[idx].size() - 1; i >= 0; i--) {\n      auto\
    \ &e = g[idx][i];\n      if(e.to != par) dfs_all(e.to, idx, f(e.ndp, buff));\n\
    \      e.ndp = f(e.ndp, buff);\n      buff = f(buff, e.dp);\n    }\n  }\n\n  vector<\
    \ sum_t > build() {\n    dfs_sub(0, -1);\n    dfs_all(0, -1, ident);\n    return\
    \ dp;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/tree/rerooting.hpp
  requiredBy: []
  timestamp: '2021-07-01 02:53:34+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-1595.test.cpp
documentation_of: graph/tree/rerooting.hpp
layout: document
redirect_from:
- /library/graph/tree/rerooting.hpp
- /library/graph/tree/rerooting.hpp.html
title: graph/tree/rerooting.hpp
---
