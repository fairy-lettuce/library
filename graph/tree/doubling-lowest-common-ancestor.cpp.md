---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':x:'
    path: test/verify/aoj-grl-5-c.test.cpp
    title: test/verify/aoj-grl-5-c.test.cpp
  - icon: ':x:'
    path: test/verify/yosupo-lca-3.test.cpp
    title: test/verify/yosupo-lca-3.test.cpp
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes:
    _deprecated_at_docs: docs/doubling-lowest-common-ancestor.md
    document_title: "Doubling-Lowest-Common-Ancestor(\u6700\u5C0F\u5171\u901A\u7956\
      \u5148)"
    links: []
  bundledCode: "#line 1 \"graph/tree/doubling-lowest-common-ancestor.cpp\"\n/**\n\
    \ * @brief Doubling-Lowest-Common-Ancestor(\u6700\u5C0F\u5171\u901A\u7956\u5148\
    )\n * @docs docs/doubling-lowest-common-ancestor.md\n */\ntemplate< typename T\
    \ >\nstruct DoublingLowestCommonAncestor : Graph< T > {\npublic:\n  using Graph<\
    \ T >::g;\n  vector< int > dep;\n  vector< T > sum;\n  vector< vector< int > >\
    \ table;\n  const int LOG;\n\n  explicit DoublingLowestCommonAncestor(int n)\n\
    \      : LOG(32 - __builtin_clz(g.size())), Graph< T >(n) {}\n\n  explicit DoublingLowestCommonAncestor(const\
    \ Graph< T > &g)\n      : LOG(32 - __builtin_clz(g.size())), Graph< T >(g) {}\n\
    \n  void build() {\n    dep.assign(g.size(), 0);\n    sum.assign(g.size(), 0);\n\
    \    table.assign(LOG, vector< int >(g.size(), -1));\n    dfs(0, -1, 0);\n   \
    \ for(int k = 0; k + 1 < LOG; k++) {\n      for(int i = 0; i < table[k].size();\
    \ i++) {\n        if(table[k][i] == -1) table[k + 1][i] = -1;\n        else table[k\
    \ + 1][i] = table[k][table[k][i]];\n      }\n    }\n  }\n\n  int lca(int u, int\
    \ v) {\n    if(dep[u] > dep[v]) swap(u, v);\n    v = climb(v, dep[v] - dep[u]);\n\
    \    if(u == v) return u;\n    for(int i = LOG - 1; i >= 0; i--) {\n      if(table[i][u]\
    \ != table[i][v]) {\n        u = table[i][u];\n        v = table[i][v];\n    \
    \  }\n    }\n    return table[0][u];\n  }\n\n  int climb(int u, int k) const {\n\
    \    if(dep[u] < k) return -1;\n    for(int i = LOG - 1; i >= 0; i--) {\n    \
    \  if((k >> i) & 1) u = table[i][u];\n    }\n    return u;\n  }\n\n  T dist(int\
    \ u, int v) const {\n    return sum[u] + sum[v] - 2 * sum[lca(u, v)];\n  }\n\n\
    private:\n  void dfs(int idx, int par, int d) {\n    table[0][idx] = par;\n  \
    \  dep[idx] = d;\n    for(auto &to : g[idx]) {\n      if(to != par) {\n      \
    \  sum[to] = sum[idx] + to.cost;\n        dfs(to, idx, d + 1);\n      }\n    }\n\
    \  }\n};\n"
  code: "/**\n * @brief Doubling-Lowest-Common-Ancestor(\u6700\u5C0F\u5171\u901A\u7956\
    \u5148)\n * @docs docs/doubling-lowest-common-ancestor.md\n */\ntemplate< typename\
    \ T >\nstruct DoublingLowestCommonAncestor : Graph< T > {\npublic:\n  using Graph<\
    \ T >::g;\n  vector< int > dep;\n  vector< T > sum;\n  vector< vector< int > >\
    \ table;\n  const int LOG;\n\n  explicit DoublingLowestCommonAncestor(int n)\n\
    \      : LOG(32 - __builtin_clz(g.size())), Graph< T >(n) {}\n\n  explicit DoublingLowestCommonAncestor(const\
    \ Graph< T > &g)\n      : LOG(32 - __builtin_clz(g.size())), Graph< T >(g) {}\n\
    \n  void build() {\n    dep.assign(g.size(), 0);\n    sum.assign(g.size(), 0);\n\
    \    table.assign(LOG, vector< int >(g.size(), -1));\n    dfs(0, -1, 0);\n   \
    \ for(int k = 0; k + 1 < LOG; k++) {\n      for(int i = 0; i < table[k].size();\
    \ i++) {\n        if(table[k][i] == -1) table[k + 1][i] = -1;\n        else table[k\
    \ + 1][i] = table[k][table[k][i]];\n      }\n    }\n  }\n\n  int lca(int u, int\
    \ v) {\n    if(dep[u] > dep[v]) swap(u, v);\n    v = climb(v, dep[v] - dep[u]);\n\
    \    if(u == v) return u;\n    for(int i = LOG - 1; i >= 0; i--) {\n      if(table[i][u]\
    \ != table[i][v]) {\n        u = table[i][u];\n        v = table[i][v];\n    \
    \  }\n    }\n    return table[0][u];\n  }\n\n  int climb(int u, int k) const {\n\
    \    if(dep[u] < k) return -1;\n    for(int i = LOG - 1; i >= 0; i--) {\n    \
    \  if((k >> i) & 1) u = table[i][u];\n    }\n    return u;\n  }\n\n  T dist(int\
    \ u, int v) const {\n    return sum[u] + sum[v] - 2 * sum[lca(u, v)];\n  }\n\n\
    private:\n  void dfs(int idx, int par, int d) {\n    table[0][idx] = par;\n  \
    \  dep[idx] = d;\n    for(auto &to : g[idx]) {\n      if(to != par) {\n      \
    \  sum[to] = sum[idx] + to.cost;\n        dfs(to, idx, d + 1);\n      }\n    }\n\
    \  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/tree/doubling-lowest-common-ancestor.cpp
  requiredBy: []
  timestamp: '2020-11-10 01:30:09+09:00'
  verificationStatus: LIBRARY_ALL_WA
  verifiedWith:
  - test/verify/aoj-grl-5-c.test.cpp
  - test/verify/yosupo-lca-3.test.cpp
documentation_of: graph/tree/doubling-lowest-common-ancestor.cpp
layout: document
redirect_from:
- /library/graph/tree/doubling-lowest-common-ancestor.cpp
- /library/graph/tree/doubling-lowest-common-ancestor.cpp.html
title: "Doubling-Lowest-Common-Ancestor(\u6700\u5C0F\u5171\u901A\u7956\u5148)"
---
## 概要
ダブリングによって最小共通祖先を求める.

頂点 $u$, $v$ の最小共通祖先を求めたいとする. $dep[i]$ をある頂点を根とする根付き木としてみたときの深さとし, $dep[u] \leq dep[v]$ を仮定する. まず $dep[v] - dep[u]$ 個だけ頂点 $v$ を親に遡らせて, 頂点 $u, v$ の深さを揃える. このとき深さが一致したらそれが最小共通祖先. それ以外のとき, 上位 bit から頂点 $u, v$ 双方の $2^k$ 個先の親を見て, 異なれば遡ることを繰り返し, 双方の親ではない直前の頂点を求める. するとその親が最小共通祖先であることがわかる.

## 使い方

* `build()`: 構築する.
* `lca(u, v)`: 頂点 `u`, `v` の最小共通祖先(LCA)を返す.
* `climb(u, k)`: 頂点 `u` から `k` 個親に遡った頂点を返す.
* `dist(u, v)`: 頂点 `u`, `v` 間のパスの辺の本数を返す.

## 計算量

* `build()`: $O(V)$
* `lca()`, `climb(u, k)`, `dist()`: $O(\log V)$
