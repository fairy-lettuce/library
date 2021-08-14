---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-grl-6-a-4.test.cpp
    title: test/verify/aoj-grl-6-a-4.test.cpp
  _isVerificationFailed: false
  _pathExtension: hpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/dinic-capacity-scaling.md
    document_title: "Dinic Capacity Scaling(\u6700\u5927\u6D41)"
    links: []
  bundledCode: "#line 1 \"graph/flow/dinic-capacity-scaling.hpp\"\n/**\n * @brief\
    \ Dinic Capacity Scaling(\u6700\u5927\u6D41)\n * @docs docs/dinic-capacity-scaling.md\n\
    \ */\ntemplate< typename flow_t >\nstruct DinicCapacityScaling {\n  static_assert(is_integral<\
    \ flow_t >::value, \"template parameter flow_t must be integral type\");\n\n \
    \ const flow_t INF;\n\n  struct edge {\n    int to;\n    flow_t cap;\n    int\
    \ rev;\n    bool isrev;\n    int idx;\n  };\n\n  vector< vector< edge > > graph;\n\
    \  vector< int > min_cost, iter;\n  flow_t max_cap;\n\n  explicit DinicCapacityScaling(int\
    \ V) : INF(numeric_limits< flow_t >::max()), graph(V), max_cap(0) {}\n\n  void\
    \ add_edge(int from, int to, flow_t cap, int idx = -1) {\n    max_cap = max(max_cap,\
    \ cap);\n    graph[from].emplace_back((edge) {to, cap, (int) graph[to].size(),\
    \ false, idx});\n    graph[to].emplace_back((edge) {from, 0, (int) graph[from].size()\
    \ - 1, true, idx});\n  }\n\n  bool build_augment_path(int s, int t, const flow_t\
    \ &base) {\n    min_cost.assign(graph.size(), -1);\n    queue< int > que;\n  \
    \  min_cost[s] = 0;\n    que.push(s);\n    while(!que.empty() && min_cost[t] ==\
    \ -1) {\n      int p = que.front();\n      que.pop();\n      for(auto &e : graph[p])\
    \ {\n        if(e.cap >= base && min_cost[e.to] == -1) {\n          min_cost[e.to]\
    \ = min_cost[p] + 1;\n          que.push(e.to);\n        }\n      }\n    }\n \
    \   return min_cost[t] != -1;\n  }\n\n  flow_t find_augment_path(int idx, const\
    \ int t, flow_t base, flow_t flow) {\n    if(idx == t) return flow;\n    flow_t\
    \ sum = 0;\n    for(int &i = iter[idx]; i < (int)graph[idx].size(); i++) {\n \
    \     edge &e = graph[idx][i];\n      if(e.cap >= base && min_cost[idx] < min_cost[e.to])\
    \ {\n        flow_t d = find_augment_path(e.to, t, base, min(flow - sum, e.cap));\n\
    \        if(d > 0) {\n          e.cap -= d;\n          graph[e.to][e.rev].cap\
    \ += d;\n          sum += d;\n          if(flow - sum < base) break;\n       \
    \ }\n      }\n    }\n    return sum;\n  }\n\n  flow_t max_flow(int s, int t) {\n\
    \    if(max_cap == flow_t(0)) return flow_t(0);\n    flow_t flow = 0;\n    for(int\
    \ i = 63 - __builtin_clzll(max_cap); i >= 0; i--) {\n      flow_t now = flow_t(1)\
    \ << i;\n      while(build_augment_path(s, t, now)) {\n        iter.assign(graph.size(),\
    \ 0);\n        flow += find_augment_path(s, t, now, INF);\n      }\n    }\n  \
    \  return flow;\n  }\n\n  void output() {\n    for(int i = 0; i < graph.size();\
    \ i++) {\n      for(auto &e : graph[i]) {\n        if(e.isrev) continue;\n   \
    \     auto &rev_e = graph[e.to][e.rev];\n        cout << i << \"->\" << e.to <<\
    \ \" (flow: \" << rev_e.cap << \"/\" << e.cap + rev_e.cap << \")\" << endl;\n\
    \      }\n    }\n  }\n};\n"
  code: "/**\n * @brief Dinic Capacity Scaling(\u6700\u5927\u6D41)\n * @docs docs/dinic-capacity-scaling.md\n\
    \ */\ntemplate< typename flow_t >\nstruct DinicCapacityScaling {\n  static_assert(is_integral<\
    \ flow_t >::value, \"template parameter flow_t must be integral type\");\n\n \
    \ const flow_t INF;\n\n  struct edge {\n    int to;\n    flow_t cap;\n    int\
    \ rev;\n    bool isrev;\n    int idx;\n  };\n\n  vector< vector< edge > > graph;\n\
    \  vector< int > min_cost, iter;\n  flow_t max_cap;\n\n  explicit DinicCapacityScaling(int\
    \ V) : INF(numeric_limits< flow_t >::max()), graph(V), max_cap(0) {}\n\n  void\
    \ add_edge(int from, int to, flow_t cap, int idx = -1) {\n    max_cap = max(max_cap,\
    \ cap);\n    graph[from].emplace_back((edge) {to, cap, (int) graph[to].size(),\
    \ false, idx});\n    graph[to].emplace_back((edge) {from, 0, (int) graph[from].size()\
    \ - 1, true, idx});\n  }\n\n  bool build_augment_path(int s, int t, const flow_t\
    \ &base) {\n    min_cost.assign(graph.size(), -1);\n    queue< int > que;\n  \
    \  min_cost[s] = 0;\n    que.push(s);\n    while(!que.empty() && min_cost[t] ==\
    \ -1) {\n      int p = que.front();\n      que.pop();\n      for(auto &e : graph[p])\
    \ {\n        if(e.cap >= base && min_cost[e.to] == -1) {\n          min_cost[e.to]\
    \ = min_cost[p] + 1;\n          que.push(e.to);\n        }\n      }\n    }\n \
    \   return min_cost[t] != -1;\n  }\n\n  flow_t find_augment_path(int idx, const\
    \ int t, flow_t base, flow_t flow) {\n    if(idx == t) return flow;\n    flow_t\
    \ sum = 0;\n    for(int &i = iter[idx]; i < (int)graph[idx].size(); i++) {\n \
    \     edge &e = graph[idx][i];\n      if(e.cap >= base && min_cost[idx] < min_cost[e.to])\
    \ {\n        flow_t d = find_augment_path(e.to, t, base, min(flow - sum, e.cap));\n\
    \        if(d > 0) {\n          e.cap -= d;\n          graph[e.to][e.rev].cap\
    \ += d;\n          sum += d;\n          if(flow - sum < base) break;\n       \
    \ }\n      }\n    }\n    return sum;\n  }\n\n  flow_t max_flow(int s, int t) {\n\
    \    if(max_cap == flow_t(0)) return flow_t(0);\n    flow_t flow = 0;\n    for(int\
    \ i = 63 - __builtin_clzll(max_cap); i >= 0; i--) {\n      flow_t now = flow_t(1)\
    \ << i;\n      while(build_augment_path(s, t, now)) {\n        iter.assign(graph.size(),\
    \ 0);\n        flow += find_augment_path(s, t, now, INF);\n      }\n    }\n  \
    \  return flow;\n  }\n\n  void output() {\n    for(int i = 0; i < graph.size();\
    \ i++) {\n      for(auto &e : graph[i]) {\n        if(e.isrev) continue;\n   \
    \     auto &rev_e = graph[e.to][e.rev];\n        cout << i << \"->\" << e.to <<\
    \ \" (flow: \" << rev_e.cap << \"/\" << e.cap + rev_e.cap << \")\" << endl;\n\
    \      }\n    }\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/flow/dinic-capacity-scaling.hpp
  requiredBy: []
  timestamp: '2021-08-14 14:18:51+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-grl-6-a-4.test.cpp
documentation_of: graph/flow/dinic-capacity-scaling.hpp
layout: document
redirect_from:
- /library/graph/flow/dinic-capacity-scaling.hpp
- /library/graph/flow/dinic-capacity-scaling.hpp.html
title: "Dinic Capacity Scaling(\u6700\u5927\u6D41)"
---
## 概要

最大流を求めるアルゴリズム.

すべての辺の容量が整数の場合, スケーリングを用いて Dinic の計算量を $O(EV \log U)$ に落とすことが出来る($U$ は辺の容量の最大値).

具体的には, フローを残余グラフ上で $k$ が大きい方から $2^k$ 単位で流すようにする.


## 使い方

* `DinicCapacityScaling(V)`: 頂点数 `V` で初期化する.
* `add_edge(from, to, cap, idx = -1)`: 頂点 `from` から `to` に容量 `cap` の辺を追加する.
* `max_flow(s, t)`: 頂点 `s` から `t` に最大流を流し, その流量を返す.

## 計算量

$O(EV \log U)$

$U$ は辺の容量の最大値
