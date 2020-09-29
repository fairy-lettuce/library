---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-k-shortest-walk.test.cpp
    title: test/verify/yosupo-k-shortest-walk.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/k-shortest-walk.md
    document_title: K-Shortest-Walk
    links:
    - https://qiita.com/hotman78/items/42534a01c4bd05ed5e1e
  bundledCode: "#line 1 \"graph/shortest-path/k-shortest-walk.cpp\"\n/**\n * @brief\
    \ K-Shortest-Walk\n * @docs docs/k-shortest-walk.md\n * @see https://qiita.com/hotman78/items/42534a01c4bd05ed5e1e\n\
    \ */\ntemplate< typename T >\nvector< T > k_shortest_walk(const Graph< T > &g,\
    \ int s, int t, int k) {\n  int N = (int) g.size();\n  Graph< T > rg(N);\n  for(int\
    \ i = 0; i < N; i++) {\n    for(auto &e : g.g[i]) rg.add_directed_edge(e.to, i,\
    \ e.cost);\n  }\n  auto dist = dijkstra(rg, t);\n  if(dist.from[s] == -1) return\
    \ {};\n  auto &p = dist.dist;\n  vector< vector< int > > ch(N);\n  for(int i =\
    \ 0; i < N; i++) {\n    if(dist.from[i] >= 0) ch[dist.from[i]].emplace_back(i);\n\
    \  }\n  using PHeap = PersistentLeftistHeap< T >;\n  using Node = typename PHeap::Node;\n\
    \  PHeap heap;\n  vector< Node * > h(N, heap.make_root());\n  {\n    queue< int\
    \ > que;\n    que.emplace(t);\n    while(!que.empty()) {\n      int idx = que.front();\n\
    \      que.pop();\n      if(dist.from[idx] >= 0) {\n        h[idx] = heap.meld(h[idx],\
    \ h[dist.from[idx]]);\n      }\n      bool used = true;\n      for(auto &e : g.g[idx])\
    \ {\n        if(e.to != t && dist.from[e.to] == -1) continue;\n        if(used\
    \ && dist.from[idx] == e.to && p[e.to] + e.cost == p[idx]) {\n          used =\
    \ false;\n          continue;\n        }\n        h[idx] = heap.push(h[idx], e.cost\
    \ - p[idx] + p[e.to], e.to);\n      }\n      for(auto &to : ch[idx]) que.emplace(to);\n\
    \    }\n  }\n  using pi = pair< T, Node * >;\n  auto comp = [](const pi &x, const\
    \ pi &y) { return x.first > y.first; };\n  priority_queue< pi, vector< pi >, decltype(comp)\
    \ > que(comp);\n  Node *root = heap.make_root();\n  root = heap.push(root, p[s],\
    \ s);\n  que.emplace(p[s], root);\n  vector< T > ans;\n  while(!que.empty()) {\n\
    \    T cost;\n    Node *cur;\n    tie(cost, cur) = que.top();\n    que.pop();\n\
    \    ans.emplace_back(cost);\n    if(ans.size() == k) break;\n    if(cur->l) que.emplace(cost\
    \ + cur->l->key - cur->key, cur->l);\n    if(cur->r) que.emplace(cost + cur->r->key\
    \ - cur->key, cur->r);\n    if(h[cur->idx]) que.emplace(cost + h[cur->idx]->key,\
    \ h[cur->idx]);\n  }\n  return ans;\n}\n"
  code: "/**\n * @brief K-Shortest-Walk\n * @docs docs/k-shortest-walk.md\n * @see\
    \ https://qiita.com/hotman78/items/42534a01c4bd05ed5e1e\n */\ntemplate< typename\
    \ T >\nvector< T > k_shortest_walk(const Graph< T > &g, int s, int t, int k) {\n\
    \  int N = (int) g.size();\n  Graph< T > rg(N);\n  for(int i = 0; i < N; i++)\
    \ {\n    for(auto &e : g.g[i]) rg.add_directed_edge(e.to, i, e.cost);\n  }\n \
    \ auto dist = dijkstra(rg, t);\n  if(dist.from[s] == -1) return {};\n  auto &p\
    \ = dist.dist;\n  vector< vector< int > > ch(N);\n  for(int i = 0; i < N; i++)\
    \ {\n    if(dist.from[i] >= 0) ch[dist.from[i]].emplace_back(i);\n  }\n  using\
    \ PHeap = PersistentLeftistHeap< T >;\n  using Node = typename PHeap::Node;\n\
    \  PHeap heap;\n  vector< Node * > h(N, heap.make_root());\n  {\n    queue< int\
    \ > que;\n    que.emplace(t);\n    while(!que.empty()) {\n      int idx = que.front();\n\
    \      que.pop();\n      if(dist.from[idx] >= 0) {\n        h[idx] = heap.meld(h[idx],\
    \ h[dist.from[idx]]);\n      }\n      bool used = true;\n      for(auto &e : g.g[idx])\
    \ {\n        if(e.to != t && dist.from[e.to] == -1) continue;\n        if(used\
    \ && dist.from[idx] == e.to && p[e.to] + e.cost == p[idx]) {\n          used =\
    \ false;\n          continue;\n        }\n        h[idx] = heap.push(h[idx], e.cost\
    \ - p[idx] + p[e.to], e.to);\n      }\n      for(auto &to : ch[idx]) que.emplace(to);\n\
    \    }\n  }\n  using pi = pair< T, Node * >;\n  auto comp = [](const pi &x, const\
    \ pi &y) { return x.first > y.first; };\n  priority_queue< pi, vector< pi >, decltype(comp)\
    \ > que(comp);\n  Node *root = heap.make_root();\n  root = heap.push(root, p[s],\
    \ s);\n  que.emplace(p[s], root);\n  vector< T > ans;\n  while(!que.empty()) {\n\
    \    T cost;\n    Node *cur;\n    tie(cost, cur) = que.top();\n    que.pop();\n\
    \    ans.emplace_back(cost);\n    if(ans.size() == k) break;\n    if(cur->l) que.emplace(cost\
    \ + cur->l->key - cur->key, cur->l);\n    if(cur->r) que.emplace(cost + cur->r->key\
    \ - cur->key, cur->r);\n    if(h[cur->idx]) que.emplace(cost + h[cur->idx]->key,\
    \ h[cur->idx]);\n  }\n  return ans;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/shortest-path/k-shortest-walk.cpp
  requiredBy: []
  timestamp: '2020-08-21 01:30:35+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-k-shortest-walk.test.cpp
documentation_of: graph/shortest-path/k-shortest-walk.cpp
layout: document
redirect_from:
- /library/graph/shortest-path/k-shortest-walk.cpp
- /library/graph/shortest-path/k-shortest-walk.cpp.html
title: K-Shortest-Walk
---
## 概要

頂点 $s$ から $t$ へのウォーク(Walk) のうち, 昇順 $k$ 個のウォークの長さを Eppstein's Algorithm により求める. 

ウォーク(Walk, 歩道, 経路) とは重複して頂点や辺が現れることを許容した頂点 $s$ から $t$ への経路を指す.

ちなみにトレイル(Trail) は同じ辺を通らない経路, 道(Path) は同じ頂点を通らない経路である.

* `k_shotest_walk(g, s, t, k)`: 重み付き有向グラフ `g` の頂点 `s` から `t` へのウォークのうち, 昇順 `k` 個のウォークの長さを返す(ウォークの個数が `k` 個に満たないとき全てを返す).

## 計算量

* $O((V + E) \log V + K \log K)$
