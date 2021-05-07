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
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/bellman-ford.md
    document_title: "Bellman-Ford(\u5358\u4E00\u59CB\u70B9\u6700\u77ED\u8DEF)"
    links: []
  bundledCode: "#line 1 \"graph/shortest-path/bellman-ford.cpp\"\n/**\n * @brief Bellman-Ford(\u5358\
    \u4E00\u59CB\u70B9\u6700\u77ED\u8DEF)\n * @docs docs/bellman-ford.md\n */\ntemplate<\
    \ typename T >\nvector< T > bellman_ford(const Edges< T > &edges, int V, int s)\
    \ {\n  const auto INF = numeric_limits< T >::max();\n  vector< T > dist(V, INF);\n\
    \  dist[s] = 0;\n  for(int i = 0; i < V - 1; i++) {\n    for(auto &e : edges)\
    \ {\n      if(dist[e.from] == INF) continue;\n      dist[e.to] = min(dist[e.to],\
    \ dist[e.from] + e.cost);\n    }\n  }\n  for(auto &e : edges) {\n    if(dist[e.from]\
    \ == INF) continue;\n    if(dist[e.from] + e.cost < dist[e.to]) return vector<\
    \ T >();\n  }\n  return dist;\n}\n"
  code: "/**\n * @brief Bellman-Ford(\u5358\u4E00\u59CB\u70B9\u6700\u77ED\u8DEF)\n\
    \ * @docs docs/bellman-ford.md\n */\ntemplate< typename T >\nvector< T > bellman_ford(const\
    \ Edges< T > &edges, int V, int s) {\n  const auto INF = numeric_limits< T >::max();\n\
    \  vector< T > dist(V, INF);\n  dist[s] = 0;\n  for(int i = 0; i < V - 1; i++)\
    \ {\n    for(auto &e : edges) {\n      if(dist[e.from] == INF) continue;\n   \
    \   dist[e.to] = min(dist[e.to], dist[e.from] + e.cost);\n    }\n  }\n  for(auto\
    \ &e : edges) {\n    if(dist[e.from] == INF) continue;\n    if(dist[e.from] +\
    \ e.cost < dist[e.to]) return vector< T >();\n  }\n  return dist;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/shortest-path/bellman-ford.cpp
  requiredBy: []
  timestamp: '2020-10-07 14:06:33+09:00'
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
## 概要

単一始点全点間最短路を求めるアルゴリズム. 負辺があっても動作する. また負閉路も検出する.

負閉路がない場合, 全ての頂点への最短路に含まれる辺の本数は $V - 1$ 本以下である. したがって $V - 1$ 回すべての辺を走査して最短路を更新すると, 最終的な最短路が求まる.

負閉路がある場合 $V$ 回目に更新があるときだが, 始点とある頂点との $2$ 点間のパスに負閉路が含まれることと同値ではないので注意すること(これを判定した場合は負閉路からその頂点に到達可能か判定するか, 始点とある頂点から到達できない頂点を予め削除しておく必要がある, 実装しなさーい！).

## 使い方
* `bellman_ford(g, V, s)`: `V` 頂点の重み付きグラフ `g` で, 頂点 `s` から全点間の最短コストを求める.

## 計算量

* $O(VE)$
