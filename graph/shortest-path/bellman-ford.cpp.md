---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-0304.test.cpp
    title: test/verify/aoj-0304.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-grl-1-b.test.cpp
    title: test/verify/aoj-grl-1-b.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    document_title: "Bellman-Ford(\u5358\u4E00\u59CB\u70B9\u6700\u77ED\u8DEF)"
    links: []
  bundledCode: "#line 1 \"graph/shortest-path/bellman-ford.cpp\"\n/**\n * @brief Bellman-Ford(\u5358\
    \u4E00\u59CB\u70B9\u6700\u77ED\u8DEF)\n */\ntemplate< typename T >\nvector< T\
    \ > bellman_ford(const Edges< T > &edges, int V, int s) {\n  const auto INF =\
    \ numeric_limits< T >::max();\n  vector< T > dist(V, INF);\n  dist[s] = 0;\n \
    \ for(int i = 0; i < V - 1; i++) {\n    for(auto &e : edges) {\n      if(dist[e.from]\
    \ == INF) continue;\n      dist[e.to] = min(dist[e.to], dist[e.from] + e.cost);\n\
    \    }\n  }\n  for(auto &e : edges) {\n    if(dist[e.from] == INF) continue;\n\
    \    if(dist[e.from] + e.cost < dist[e.to]) return vector< T >();\n  }\n  return\
    \ dist;\n}\n"
  code: "/**\n * @brief Bellman-Ford(\u5358\u4E00\u59CB\u70B9\u6700\u77ED\u8DEF)\n\
    \ */\ntemplate< typename T >\nvector< T > bellman_ford(const Edges< T > &edges,\
    \ int V, int s) {\n  const auto INF = numeric_limits< T >::max();\n  vector< T\
    \ > dist(V, INF);\n  dist[s] = 0;\n  for(int i = 0; i < V - 1; i++) {\n    for(auto\
    \ &e : edges) {\n      if(dist[e.from] == INF) continue;\n      dist[e.to] = min(dist[e.to],\
    \ dist[e.from] + e.cost);\n    }\n  }\n  for(auto &e : edges) {\n    if(dist[e.from]\
    \ == INF) continue;\n    if(dist[e.from] + e.cost < dist[e.to]) return vector<\
    \ T >();\n  }\n  return dist;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/shortest-path/bellman-ford.cpp
  requiredBy: []
  timestamp: '2020-03-28 20:39:54+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-0304.test.cpp
  - test/verify/aoj-grl-1-b.test.cpp
documentation_of: graph/shortest-path/bellman-ford.cpp
layout: document
redirect_from:
- /library/graph/shortest-path/bellman-ford.cpp
- /library/graph/shortest-path/bellman-ford.cpp.html
title: "Bellman-Ford(\u5358\u4E00\u59CB\u70B9\u6700\u77ED\u8DEF)"
---
