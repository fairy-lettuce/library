---
data:
  _extendedDependsOn:
  - icon: ':question:'
    path: graph/graph-template.hpp
    title: "Graph Template(\u30B0\u30E9\u30D5\u30C6\u30F3\u30D7\u30EC\u30FC\u30C8)"
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-grl-1-a-2.test.cpp
    title: test/verify/aoj-grl-1-a-2.test.cpp
  _isVerificationFailed: false
  _pathExtension: hpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/dijkstra-fibonacchi-heap.md
    document_title: "Dijkstra-Fibonacchi-Heap(\u5358\u4E00\u59CB\u70B9\u6700\u77ED\
      \u8DEF)"
    links: []
  bundledCode: "#line 2 \"graph/shortest-path/dijkstra-fibonacchi-heap.hpp\"\n\n#line\
    \ 2 \"graph/graph-template.hpp\"\n\n/**\n * @brief Graph Template(\u30B0\u30E9\
    \u30D5\u30C6\u30F3\u30D7\u30EC\u30FC\u30C8)\n */\ntemplate< typename T = int >\n\
    struct Edge {\n  int from, to;\n  T cost;\n  int idx;\n\n  Edge() = default;\n\
    \n  Edge(int from, int to, T cost = 1, int idx = -1) : from(from), to(to), cost(cost),\
    \ idx(idx) {}\n\n  operator int() const { return to; }\n};\n\ntemplate< typename\
    \ T = int >\nstruct Graph {\n  vector< vector< Edge< T > > > g;\n  int es;\n\n\
    \  Graph() = default;\n\n  explicit Graph(int n) : g(n), es(0) {}\n\n  size_t\
    \ size() const {\n    return g.size();\n  }\n\n  void add_directed_edge(int from,\
    \ int to, T cost = 1) {\n    g[from].emplace_back(from, to, cost, es++);\n  }\n\
    \n  void add_edge(int from, int to, T cost = 1) {\n    g[from].emplace_back(from,\
    \ to, cost, es);\n    g[to].emplace_back(to, from, cost, es++);\n  }\n\n  void\
    \ read(int M, int padding = -1, bool weighted = false, bool directed = false)\
    \ {\n    for(int i = 0; i < M; i++) {\n      int a, b;\n      cin >> a >> b;\n\
    \      a += padding;\n      b += padding;\n      T c = T(1);\n      if(weighted)\
    \ cin >> c;\n      if(directed) add_directed_edge(a, b, c);\n      else add_edge(a,\
    \ b, c);\n    }\n  }\n\n  inline vector< Edge< T > > &operator[](const int &k)\
    \ {\n    return g[k];\n  }\n\n  inline const vector< Edge< T > > &operator[](const\
    \ int &k) const {\n    return g[k];\n  }\n};\n\ntemplate< typename T = int >\n\
    using Edges = vector< Edge< T > >;\n#line 4 \"graph/shortest-path/dijkstra-fibonacchi-heap.hpp\"\
    \n\n/**\n * @brief Dijkstra-Fibonacchi-Heap(\u5358\u4E00\u59CB\u70B9\u6700\u77ED\
    \u8DEF)\n * @docs docs/dijkstra-fibonacchi-heap.md\n */\ntemplate< typename T\
    \ >\nvector< T > dijkstra_fibonacchi_heap(Graph< T > &g, int s) {\n  const auto\
    \ INF = numeric_limits< T >::max();\n  using Heap = FibonacchiHeap< T, int >;\n\
    \  using Node = typename Heap::Node;\n\n  Heap heap;\n  vector< Node * > keep(g.size(),\
    \ nullptr);\n  vector< T > dist;\n  dist.assign(g.size(), INF);\n  dist[s] = 0;\n\
    \  keep[s] = heap.push(dist[s], s);\n\n  while(!heap.empty()) {\n    T cost;\n\
    \    int idx;\n    tie(cost, idx) = heap.pop();\n    if(dist[idx] < cost) continue;\n\
    \    for(auto &e : g[idx]) {\n      auto next_cost = cost + e.cost;\n      if(dist[e.to]\
    \ <= next_cost) continue;\n      if(keep[e.to] == nullptr) {\n        dist[e.to]\
    \ = next_cost;\n        keep[e.to] = heap.push(dist[e.to], e.to);\n      } else\
    \ {\n        T d = dist[e.to] - next_cost;\n        heap.decrease_key(keep[e.to],\
    \ d);\n        dist[e.to] -= d;\n      }\n    }\n  }\n  return dist;\n}\n"
  code: "#pragma once\n\n#include \"../graph-template.hpp\"\n\n/**\n * @brief Dijkstra-Fibonacchi-Heap(\u5358\
    \u4E00\u59CB\u70B9\u6700\u77ED\u8DEF)\n * @docs docs/dijkstra-fibonacchi-heap.md\n\
    \ */\ntemplate< typename T >\nvector< T > dijkstra_fibonacchi_heap(Graph< T >\
    \ &g, int s) {\n  const auto INF = numeric_limits< T >::max();\n  using Heap =\
    \ FibonacchiHeap< T, int >;\n  using Node = typename Heap::Node;\n\n  Heap heap;\n\
    \  vector< Node * > keep(g.size(), nullptr);\n  vector< T > dist;\n  dist.assign(g.size(),\
    \ INF);\n  dist[s] = 0;\n  keep[s] = heap.push(dist[s], s);\n\n  while(!heap.empty())\
    \ {\n    T cost;\n    int idx;\n    tie(cost, idx) = heap.pop();\n    if(dist[idx]\
    \ < cost) continue;\n    for(auto &e : g[idx]) {\n      auto next_cost = cost\
    \ + e.cost;\n      if(dist[e.to] <= next_cost) continue;\n      if(keep[e.to]\
    \ == nullptr) {\n        dist[e.to] = next_cost;\n        keep[e.to] = heap.push(dist[e.to],\
    \ e.to);\n      } else {\n        T d = dist[e.to] - next_cost;\n        heap.decrease_key(keep[e.to],\
    \ d);\n        dist[e.to] -= d;\n      }\n    }\n  }\n  return dist;\n}\n"
  dependsOn:
  - graph/graph-template.hpp
  isVerificationFile: false
  path: graph/shortest-path/dijkstra-fibonacchi-heap.hpp
  requiredBy: []
  timestamp: '2021-08-16 02:34:50+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-grl-1-a-2.test.cpp
documentation_of: graph/shortest-path/dijkstra-fibonacchi-heap.hpp
layout: document
redirect_from:
- /library/graph/shortest-path/dijkstra-fibonacchi-heap.hpp
- /library/graph/shortest-path/dijkstra-fibonacchi-heap.hpp.html
title: "Dijkstra-Fibonacchi-Heap(\u5358\u4E00\u59CB\u70B9\u6700\u77ED\u8DEF)"
---
## 概要

負辺のないグラフで単一始点全点間最短路を求めるアルゴリズム.

通常の dijkstra 法では `std::priority_queue` を使用していたが, これをフィボナッチヒープにすることで計算量を落とせる(実用上早くなるかは知らない).

* `dijkstra_fibonacchi_heap(g, s)`: 重み付きグラフ `g` で, 頂点 `s` から全点間の最短距離を求める. 到達できない頂点には, 型の最大値が格納される.

## 計算量

* $O(V \log V + E)$
~

