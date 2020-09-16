---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':x:'
    path: test/verify/aoj-grl-2-a.test.cpp
    title: test/verify/aoj-grl-2-a.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    _deprecated_at_docs: docs/prim.md
    document_title: "Prim(\u6700\u5C0F\u5168\u57DF\u6728)"
    links: []
  bundledCode: "#line 1 \"graph/mst/prim.cpp\"\n/**\n * @brief Prim(\u6700\u5C0F\u5168\
    \u57DF\u6728)\n * @docs docs/prim.md\n */\ntemplate< typename T >\nstruct MinimumSpanningTree\
    \ {\n  T cost;\n  Edges< T > edges;\n};\n\ntemplate< typename T >\nMinimumSpanningTree<\
    \ T > prim(const Graph< T > &g) {\n  T total = T();\n  vector< int > used(g.size());\n\
    \  vector< Edge< T > * > dist(g.size());\n  using pi = pair< T, int >;\n  priority_queue<\
    \ pi, vector< pi >, greater<> > que;\n  que.emplace(T(), 0);\n  Edges< T > edges;\n\
    \  while(!que.empty()) {\n    auto p = que.top();\n    que.pop();\n    if(used[p.second])\
    \ continue;\n    used[p.second] = true;\n    total += p.first;\n    if(dist[p.second])\
    \ edges.emplace_back(*dist[p.second]);\n    for(auto &e : g.g[p.second]) {\n \
    \     if(used[e.to] || (dist[e.to] && dist[e.to]->cost <= e.cost)) continue;\n\
    \      que.emplace(e.cost, e.to);\n    }\n  }\n  return {total, edges};\n}\n"
  code: "/**\n * @brief Prim(\u6700\u5C0F\u5168\u57DF\u6728)\n * @docs docs/prim.md\n\
    \ */\ntemplate< typename T >\nstruct MinimumSpanningTree {\n  T cost;\n  Edges<\
    \ T > edges;\n};\n\ntemplate< typename T >\nMinimumSpanningTree< T > prim(const\
    \ Graph< T > &g) {\n  T total = T();\n  vector< int > used(g.size());\n  vector<\
    \ Edge< T > * > dist(g.size());\n  using pi = pair< T, int >;\n  priority_queue<\
    \ pi, vector< pi >, greater<> > que;\n  que.emplace(T(), 0);\n  Edges< T > edges;\n\
    \  while(!que.empty()) {\n    auto p = que.top();\n    que.pop();\n    if(used[p.second])\
    \ continue;\n    used[p.second] = true;\n    total += p.first;\n    if(dist[p.second])\
    \ edges.emplace_back(*dist[p.second]);\n    for(auto &e : g.g[p.second]) {\n \
    \     if(used[e.to] || (dist[e.to] && dist[e.to]->cost <= e.cost)) continue;\n\
    \      que.emplace(e.cost, e.to);\n    }\n  }\n  return {total, edges};\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/mst/prim.cpp
  requiredBy: []
  timestamp: '2020-08-10 20:09:21+09:00'
  verificationStatus: LIBRARY_ALL_WA
  verifiedWith:
  - test/verify/aoj-grl-2-a.test.cpp
documentation_of: graph/mst/prim.cpp
layout: document
redirect_from:
- /library/graph/mst/prim.cpp
- /library/graph/mst/prim.cpp.html
title: "Prim(\u6700\u5C0F\u5168\u57DF\u6728)"
---
## 概要

最小全域木(全域木のうち, その辺群の重みの総和が最小になる木)を求める. 既に到達した頂点集合からまだ到達していない頂点集合への辺のうち, コストが最小のものを選んでいくことによって, 最小全域木を構成している.

* `prim(g)`: 連結な重み付きグラフ `g` の最小全域木を求める. `cost` には辺の重みの総和, `edges` にはそれを構成する辺が格納される.

## 計算量

* $O(E \log V)$ 
