---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-0275.test.cpp
    title: test/verify/aoj-0275.test.cpp
  - icon: ':x:'
    path: test/verify/aoj-grl-1-a.test.cpp
    title: test/verify/aoj-grl-1-a.test.cpp
  - icon: ':x:'
    path: test/verify/yosupo-k-shortest-walk.test.cpp
    title: test/verify/yosupo-k-shortest-walk.test.cpp
  - icon: ':x:'
    path: test/verify/yosupo-shortest-path.test.cpp
    title: test/verify/yosupo-shortest-path.test.cpp
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':question:'
  attributes:
    _deprecated_at_docs: docs/dijkstra.md
    document_title: "Dijkstra(\u5358\u4E00\u59CB\u70B9\u6700\u77ED\u8DEF)"
    links: []
  bundledCode: "#line 1 \"graph/shortest-path/dijkstra.cpp\"\n/**\n * @brief Dijkstra(\u5358\
    \u4E00\u59CB\u70B9\u6700\u77ED\u8DEF)\n * @docs docs/dijkstra.md\n */\ntemplate<\
    \ typename T >\nstruct ShortestPath {\n  vector< T > dist;\n  vector< int > from,\
    \ id;\n};\n\ntemplate< typename T >\nShortestPath< T > dijkstra(const Graph< T\
    \ > &g, int s) {\n  const auto INF = numeric_limits< T >::max();\n  vector< T\
    \ > dist(g.size(), INF);\n  vector< int > from(g.size(), -1), id(g.size(), -1);\n\
    \  using Pi = pair< T, int >;\n  priority_queue< Pi, vector< Pi >, greater<> >\
    \ que;\n  dist[s] = 0;\n  que.emplace(dist[s], s);\n  while(!que.empty()) {\n\
    \    T cost;\n    int idx;\n    tie(cost, idx) = que.top();\n    que.pop();\n\
    \    if(dist[idx] < cost) continue;\n    for(auto &e : g.g[idx]) {\n      auto\
    \ next_cost = cost + e.cost;\n      if(dist[e.to] <= next_cost) continue;\n  \
    \    dist[e.to] = next_cost;\n      from[e.to] = idx;\n      id[e.to] = e.idx;\n\
    \      que.emplace(dist[e.to], e.to);\n    }\n  }\n  return {dist, from, id};\n\
    }\n"
  code: "/**\n * @brief Dijkstra(\u5358\u4E00\u59CB\u70B9\u6700\u77ED\u8DEF)\n * @docs\
    \ docs/dijkstra.md\n */\ntemplate< typename T >\nstruct ShortestPath {\n  vector<\
    \ T > dist;\n  vector< int > from, id;\n};\n\ntemplate< typename T >\nShortestPath<\
    \ T > dijkstra(const Graph< T > &g, int s) {\n  const auto INF = numeric_limits<\
    \ T >::max();\n  vector< T > dist(g.size(), INF);\n  vector< int > from(g.size(),\
    \ -1), id(g.size(), -1);\n  using Pi = pair< T, int >;\n  priority_queue< Pi,\
    \ vector< Pi >, greater<> > que;\n  dist[s] = 0;\n  que.emplace(dist[s], s);\n\
    \  while(!que.empty()) {\n    T cost;\n    int idx;\n    tie(cost, idx) = que.top();\n\
    \    que.pop();\n    if(dist[idx] < cost) continue;\n    for(auto &e : g.g[idx])\
    \ {\n      auto next_cost = cost + e.cost;\n      if(dist[e.to] <= next_cost)\
    \ continue;\n      dist[e.to] = next_cost;\n      from[e.to] = idx;\n      id[e.to]\
    \ = e.idx;\n      que.emplace(dist[e.to], e.to);\n    }\n  }\n  return {dist,\
    \ from, id};\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/shortest-path/dijkstra.cpp
  requiredBy: []
  timestamp: '2020-08-21 01:30:35+09:00'
  verificationStatus: LIBRARY_SOME_WA
  verifiedWith:
  - test/verify/aoj-grl-1-a.test.cpp
  - test/verify/aoj-0275.test.cpp
  - test/verify/yosupo-k-shortest-walk.test.cpp
  - test/verify/yosupo-shortest-path.test.cpp
documentation_of: graph/shortest-path/dijkstra.cpp
layout: document
redirect_from:
- /library/graph/shortest-path/dijkstra.cpp
- /library/graph/shortest-path/dijkstra.cpp.html
title: "Dijkstra(\u5358\u4E00\u59CB\u70B9\u6700\u77ED\u8DEF)"
---
## 概要

負辺のないグラフで単一始点全点間最短路を求めるアルゴリズム. 各地点でもっとも近い頂点から距離が確定していく. 距離順でソートされたヒープを用いると, 効率よく距離を確定していくことができる.

* `dijkstra(g, s)`: 重み付きグラフ `g` で, 頂点 `s` から全点間の最短コストを求める. `dist` には最短コスト(到達できないとき型の最大値), `from` にはその頂点の直前に訪れた頂点(頂点 `s` または到達できない頂点は $-1$), `id` はその頂点の直前に使った辺番号が格納される.

## 計算量

* $O(E \log V)$ 
