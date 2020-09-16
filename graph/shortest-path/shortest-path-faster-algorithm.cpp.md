---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-grl-1-b-2.test.cpp
    title: test/verify/aoj-grl-1-b-2.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    document_title: "Shortest-Path-Faster-Algorithm(\u5358\u4E00\u59CB\u70B9\u6700\
      \u77ED\u8DEF)"
    links: []
  bundledCode: "#line 1 \"graph/shortest-path/shortest-path-faster-algorithm.cpp\"\
    \n/**\n * @brief Shortest-Path-Faster-Algorithm(\u5358\u4E00\u59CB\u70B9\u6700\
    \u77ED\u8DEF)\n */\ntemplate< typename T >\nvector< T > shortest_path_faster_algorithm(const\
    \ Graph< T > &g, int s) {\n  const auto INF = numeric_limits< T >::max();\n  vector<\
    \ T > dist(g.size(), INF);\n  vector< int > pending(g.size(), 0), times(g.size(),\
    \ 0);\n  queue< int > que;\n\n  que.emplace(s);\n  pending[s] = true;\n  ++times[s];\n\
    \  dist[s] = 0;\n\n  while(!que.empty()) {\n    int p = que.front();\n    que.pop();\n\
    \    pending[p] = false;\n    for(auto &e : g.g[p]) {\n      T next_cost = dist[p]\
    \ + e.cost;\n      if(next_cost >= dist[e.to]) continue;\n      dist[e.to] = next_cost;\n\
    \      if(!pending[e.to]) {\n        if(++times[e.to] >= g.size()) return vector<\
    \ T >();\n        pending[e.to] = true;\n        que.emplace(e.to);\n      }\n\
    \    }\n  }\n  return dist;\n}\n"
  code: "/**\n * @brief Shortest-Path-Faster-Algorithm(\u5358\u4E00\u59CB\u70B9\u6700\
    \u77ED\u8DEF)\n */\ntemplate< typename T >\nvector< T > shortest_path_faster_algorithm(const\
    \ Graph< T > &g, int s) {\n  const auto INF = numeric_limits< T >::max();\n  vector<\
    \ T > dist(g.size(), INF);\n  vector< int > pending(g.size(), 0), times(g.size(),\
    \ 0);\n  queue< int > que;\n\n  que.emplace(s);\n  pending[s] = true;\n  ++times[s];\n\
    \  dist[s] = 0;\n\n  while(!que.empty()) {\n    int p = que.front();\n    que.pop();\n\
    \    pending[p] = false;\n    for(auto &e : g.g[p]) {\n      T next_cost = dist[p]\
    \ + e.cost;\n      if(next_cost >= dist[e.to]) continue;\n      dist[e.to] = next_cost;\n\
    \      if(!pending[e.to]) {\n        if(++times[e.to] >= g.size()) return vector<\
    \ T >();\n        pending[e.to] = true;\n        que.emplace(e.to);\n      }\n\
    \    }\n  }\n  return dist;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/shortest-path/shortest-path-faster-algorithm.cpp
  requiredBy: []
  timestamp: '2020-03-28 20:39:54+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-grl-1-b-2.test.cpp
documentation_of: graph/shortest-path/shortest-path-faster-algorithm.cpp
layout: document
redirect_from:
- /library/graph/shortest-path/shortest-path-faster-algorithm.cpp
- /library/graph/shortest-path/shortest-path-faster-algorithm.cpp.html
title: "Shortest-Path-Faster-Algorithm(\u5358\u4E00\u59CB\u70B9\u6700\u77ED\u8DEF)"
---
