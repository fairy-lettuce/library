---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-alds-1-11-c.test.cpp
    title: test/verify/aoj-alds-1-11-c.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    document_title: "BFS(\u5E45\u512A\u5148\u63A2\u7D22)"
    links: []
  bundledCode: "#line 1 \"graph/shortest-path/bfs.cpp\"\n/**\n * @brief BFS(\u5E45\
    \u512A\u5148\u63A2\u7D22)\n */\ntemplate< typename T >\nvector< T > bfs(const\
    \ Graph< T > &g, int s) {\n  T max_cost = 0, beet = 0;\n  for(auto &es : g.g)\
    \ {\n    for(auto &e : es) max_cost = max(max_cost, e.cost);\n  }\n  ++max_cost;\n\
    \  const auto INF = numeric_limits< T >::max();\n  vector< T > dist(g.size(),\
    \ INF);\n  vector< queue< int > > ques(max_cost + 1);\n  dist[s] = 0;\n  ques[0].emplace(s);\n\
    \  for(T cost = 0; cost <= beet; cost++) {\n    auto &que = ques[cost % max_cost];\n\
    \    while(!que.empty()) {\n      int idx = que.front();\n      que.pop();\n \
    \     if(dist[idx] < cost) continue;\n      for(auto &e : g.g[idx]) {\n      \
    \  auto next_cost = cost + e.cost;\n        if(dist[e.to] <= next_cost) continue;;\n\
    \        dist[e.to] = next_cost;\n        beet = max(beet, dist[e.to]);\n    \
    \    ques[dist[e.to] % max_cost].emplace(e.to);\n      }\n    }\n  }\n  return\
    \ dist;\n}\n"
  code: "/**\n * @brief BFS(\u5E45\u512A\u5148\u63A2\u7D22)\n */\ntemplate< typename\
    \ T >\nvector< T > bfs(const Graph< T > &g, int s) {\n  T max_cost = 0, beet =\
    \ 0;\n  for(auto &es : g.g) {\n    for(auto &e : es) max_cost = max(max_cost,\
    \ e.cost);\n  }\n  ++max_cost;\n  const auto INF = numeric_limits< T >::max();\n\
    \  vector< T > dist(g.size(), INF);\n  vector< queue< int > > ques(max_cost +\
    \ 1);\n  dist[s] = 0;\n  ques[0].emplace(s);\n  for(T cost = 0; cost <= beet;\
    \ cost++) {\n    auto &que = ques[cost % max_cost];\n    while(!que.empty()) {\n\
    \      int idx = que.front();\n      que.pop();\n      if(dist[idx] < cost) continue;\n\
    \      for(auto &e : g.g[idx]) {\n        auto next_cost = cost + e.cost;\n  \
    \      if(dist[e.to] <= next_cost) continue;;\n        dist[e.to] = next_cost;\n\
    \        beet = max(beet, dist[e.to]);\n        ques[dist[e.to] % max_cost].emplace(e.to);\n\
    \      }\n    }\n  }\n  return dist;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/shortest-path/bfs.cpp
  requiredBy: []
  timestamp: '2020-03-28 23:32:32+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-alds-1-11-c.test.cpp
documentation_of: graph/shortest-path/bfs.cpp
layout: document
redirect_from:
- /library/graph/shortest-path/bfs.cpp
- /library/graph/shortest-path/bfs.cpp.html
title: "BFS(\u5E45\u512A\u5148\u63A2\u7D22)"
---
