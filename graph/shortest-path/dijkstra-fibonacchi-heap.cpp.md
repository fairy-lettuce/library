---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':x:'
    path: test/verify/aoj-grl-1-a-2.test.cpp
    title: test/verify/aoj-grl-1-a-2.test.cpp
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes:
    _deprecated_at_docs: docs/dijkstra-fibonacchi-heap.md
    document_title: "Dijkstra-Fibonacchi-Heap(\u5358\u4E00\u59CB\u70B9\u6700\u77ED\
      \u8DEF)"
    links: []
  bundledCode: "#line 1 \"graph/shortest-path/dijkstra-fibonacchi-heap.cpp\"\n/**\n\
    \ * @brief Dijkstra-Fibonacchi-Heap(\u5358\u4E00\u59CB\u70B9\u6700\u77ED\u8DEF\
    )\n * @docs docs/dijkstra-fibonacchi-heap.md\n */\ntemplate< typename T >\nvector<\
    \ T > dijkstra_fibonacchi_heap(Graph< T > &g, int s) {\n  const auto INF = numeric_limits<\
    \ T >::max();\n  using Heap = FibonacchiHeap< T, int >;\n  using Node = typename\
    \ Heap::Node;\n  using Pi = pair< T, int >;\n\n  Heap heap;\n  vector< Node *\
    \ > keep(g.size(), nullptr);\n  vector< T > dist;\n  dist.assign(g.size(), INF);\n\
    \  dist[s] = 0;\n  keep[s] = heap.push(dist[s], s);\n\n  while(!heap.empty())\
    \ {\n    T cost;\n    int idx;\n    tie(cost, idx) = heap.pop();\n    if(dist[idx]\
    \ < cost) continue;\n    for(auto &e : g.g[idx]) {\n      auto next_cost = cost\
    \ + e.cost;\n      if(dist[e.to] <= next_cost) continue;\n      if(keep[e.to]\
    \ == nullptr) {\n        dist[e.to] = next_cost;\n        keep[e.to] = heap.push(dist[e.to],\
    \ e.to);\n      } else {\n        T d = dist[e.to] - next_cost;\n        heap.decrease_key(keep[e.to],\
    \ d);\n        dist[e.to] -= d;\n      }\n    }\n  }\n  return dist;\n}\n"
  code: "/**\n * @brief Dijkstra-Fibonacchi-Heap(\u5358\u4E00\u59CB\u70B9\u6700\u77ED\
    \u8DEF)\n * @docs docs/dijkstra-fibonacchi-heap.md\n */\ntemplate< typename T\
    \ >\nvector< T > dijkstra_fibonacchi_heap(Graph< T > &g, int s) {\n  const auto\
    \ INF = numeric_limits< T >::max();\n  using Heap = FibonacchiHeap< T, int >;\n\
    \  using Node = typename Heap::Node;\n  using Pi = pair< T, int >;\n\n  Heap heap;\n\
    \  vector< Node * > keep(g.size(), nullptr);\n  vector< T > dist;\n  dist.assign(g.size(),\
    \ INF);\n  dist[s] = 0;\n  keep[s] = heap.push(dist[s], s);\n\n  while(!heap.empty())\
    \ {\n    T cost;\n    int idx;\n    tie(cost, idx) = heap.pop();\n    if(dist[idx]\
    \ < cost) continue;\n    for(auto &e : g.g[idx]) {\n      auto next_cost = cost\
    \ + e.cost;\n      if(dist[e.to] <= next_cost) continue;\n      if(keep[e.to]\
    \ == nullptr) {\n        dist[e.to] = next_cost;\n        keep[e.to] = heap.push(dist[e.to],\
    \ e.to);\n      } else {\n        T d = dist[e.to] - next_cost;\n        heap.decrease_key(keep[e.to],\
    \ d);\n        dist[e.to] -= d;\n      }\n    }\n  }\n  return dist;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/shortest-path/dijkstra-fibonacchi-heap.cpp
  requiredBy: []
  timestamp: '2020-08-10 20:09:21+09:00'
  verificationStatus: LIBRARY_ALL_WA
  verifiedWith:
  - test/verify/aoj-grl-1-a-2.test.cpp
documentation_of: graph/shortest-path/dijkstra-fibonacchi-heap.cpp
layout: document
redirect_from:
- /library/graph/shortest-path/dijkstra-fibonacchi-heap.cpp
- /library/graph/shortest-path/dijkstra-fibonacchi-heap.cpp.html
title: "Dijkstra-Fibonacchi-Heap(\u5358\u4E00\u59CB\u70B9\u6700\u77ED\u8DEF)"
---
## 概要

負辺のないグラフで単一始点全点間最短路を求めるアルゴリズム.

通常の dijkstra 法では `std::priority_queue` を使用していたが, これをフィボナッチヒープにすることで計算量を落とせる(実用上早くなるかは知らない).

* `dijkstra_fibonacchi_heap(g, s)`: 重み付きグラフ `g` で, 頂点 `s` から全点間の最短距離を求める. 到達できない頂点には, 型の最大値が格納される.

## 計算量

* $O(V \log V + E)$
~

