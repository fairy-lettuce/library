---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':x:'
    path: test/verify/aoj-grl-1-a-3.test.cpp
    title: test/verify/aoj-grl-1-a-3.test.cpp
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes:
    document_title: "Dijkstra-Radix-Heap(\u5358\u4E00\u59CB\u70B9\u6700\u77ED\u8DEF\
      )"
    links: []
  bundledCode: "#line 1 \"graph/shortest-path/dijkstra-radix-heap.cpp\"\n/**\n * @brief\
    \ Dijkstra-Radix-Heap(\u5358\u4E00\u59CB\u70B9\u6700\u77ED\u8DEF)\n */\ntemplate<\
    \ typename T >\nvector< T > dijkstra_radix_heap(Graph< T > &g, int s) {\n  const\
    \ auto INF = numeric_limits< T >::max();\n  vector< T > dist(g.size(), INF);\n\
    \n  using Pi = pair< T, int >;\n  RadixHeap< T, int > heap;\n  dist[s] = 0;\n\
    \  heap.push(dist[s], s);\n  while(!heap.empty()) {\n    T cost;\n    int idx;\n\
    \    tie(cost, idx) = heap.pop();\n    if(dist[idx] < cost) continue;\n    for(auto\
    \ &e : g.g[idx]) {\n      auto next_cost = cost + e.cost;\n      if(dist[e.to]\
    \ <= next_cost) continue;\n      dist[e.to] = next_cost;\n      heap.push(dist[e.to],\
    \ e.to);\n    }\n  }\n  return dist;\n}\n"
  code: "/**\n * @brief Dijkstra-Radix-Heap(\u5358\u4E00\u59CB\u70B9\u6700\u77ED\u8DEF\
    )\n */\ntemplate< typename T >\nvector< T > dijkstra_radix_heap(Graph< T > &g,\
    \ int s) {\n  const auto INF = numeric_limits< T >::max();\n  vector< T > dist(g.size(),\
    \ INF);\n\n  using Pi = pair< T, int >;\n  RadixHeap< T, int > heap;\n  dist[s]\
    \ = 0;\n  heap.push(dist[s], s);\n  while(!heap.empty()) {\n    T cost;\n    int\
    \ idx;\n    tie(cost, idx) = heap.pop();\n    if(dist[idx] < cost) continue;\n\
    \    for(auto &e : g.g[idx]) {\n      auto next_cost = cost + e.cost;\n      if(dist[e.to]\
    \ <= next_cost) continue;\n      dist[e.to] = next_cost;\n      heap.push(dist[e.to],\
    \ e.to);\n    }\n  }\n  return dist;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/shortest-path/dijkstra-radix-heap.cpp
  requiredBy: []
  timestamp: '2020-03-26 01:02:16+09:00'
  verificationStatus: LIBRARY_ALL_WA
  verifiedWith:
  - test/verify/aoj-grl-1-a-3.test.cpp
documentation_of: graph/shortest-path/dijkstra-radix-heap.cpp
layout: document
redirect_from:
- /library/graph/shortest-path/dijkstra-radix-heap.cpp
- /library/graph/shortest-path/dijkstra-radix-heap.cpp.html
title: "Dijkstra-Radix-Heap(\u5358\u4E00\u59CB\u70B9\u6700\u77ED\u8DEF)"
---
