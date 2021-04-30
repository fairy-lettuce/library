---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':x:'
    path: test/verify/aoj-grl-6-a-2.test.cpp
    title: test/verify/aoj-grl-6-a-2.test.cpp
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes:
    _deprecated_at_docs: docs/ford-fulkerson.md
    document_title: "Ford-Fulkerson(\u6700\u5927\u6D41)"
    links: []
  bundledCode: "#line 1 \"graph/flow/ford-fulkerson.cpp\"\n/**\n * @brief Ford-Fulkerson(\u6700\
    \u5927\u6D41)\n * @docs docs/ford-fulkerson.md\n */\ntemplate< typename flow_t\
    \ >\nstruct FordFulkerson {\n  struct edge {\n    int to;\n    flow_t cap;\n \
    \   int rev;\n    bool isrev;\n    int idx;\n  };\n\n  vector< vector< edge >\
    \ > graph;\n  vector< int > used;\n  const flow_t INF;\n  int timestamp;\n\n \
    \ explicit FordFulkerson(int V) : INF(numeric_limits< flow_t >::max()), graph(V),\
    \ used(V, -1), timestamp(0) {}\n\n  void add_edge(int from, int to, flow_t cap,\
    \ int idx = -1) {\n    graph[from].emplace_back((edge) {to, cap, (int) graph[to].size(),\
    \ false, idx});\n    graph[to].emplace_back((edge) {from, 0, (int) graph[from].size()\
    \ - 1, true, idx});\n  }\n\n  flow_t find_augment_path(int idx, const int t, flow_t\
    \ flow) {\n    if(idx == t) return flow;\n    used[idx] = timestamp;\n    for(auto\
    \ &e : graph[idx]) {\n      if(e.cap > 0 && used[e.to] != timestamp) {\n     \
    \   flow_t d = find_augment_path(e.to, t, min(flow, e.cap));\n        if(d > 0)\
    \ {\n          e.cap -= d;\n          graph[e.to][e.rev].cap += d;\n         \
    \ return d;\n        }\n      }\n    }\n    return 0;\n  }\n\n  flow_t max_flow(int\
    \ s, int t) {\n    flow_t flow = 0;\n    for(flow_t f; (f = find_augment_path(s,\
    \ t, INF)) > 0; timestamp++) {\n      flow += f;\n    }\n    return flow;\n  }\n\
    \n  void output() {\n    for(int i = 0; i < graph.size(); i++) {\n      for(auto\
    \ &e : graph[i]) {\n        if(e.isrev) continue;\n        auto &rev_e = graph[e.to][e.rev];\n\
    \        cout << i << \"->\" << e.to << \" (flow: \" << rev_e.cap << \"/\" <<\
    \ e.cap + rev_e.cap << \")\" << endl;\n      }\n    }\n  }\n};\n"
  code: "/**\n * @brief Ford-Fulkerson(\u6700\u5927\u6D41)\n * @docs docs/ford-fulkerson.md\n\
    \ */\ntemplate< typename flow_t >\nstruct FordFulkerson {\n  struct edge {\n \
    \   int to;\n    flow_t cap;\n    int rev;\n    bool isrev;\n    int idx;\n  };\n\
    \n  vector< vector< edge > > graph;\n  vector< int > used;\n  const flow_t INF;\n\
    \  int timestamp;\n\n  explicit FordFulkerson(int V) : INF(numeric_limits< flow_t\
    \ >::max()), graph(V), used(V, -1), timestamp(0) {}\n\n  void add_edge(int from,\
    \ int to, flow_t cap, int idx = -1) {\n    graph[from].emplace_back((edge) {to,\
    \ cap, (int) graph[to].size(), false, idx});\n    graph[to].emplace_back((edge)\
    \ {from, 0, (int) graph[from].size() - 1, true, idx});\n  }\n\n  flow_t find_augment_path(int\
    \ idx, const int t, flow_t flow) {\n    if(idx == t) return flow;\n    used[idx]\
    \ = timestamp;\n    for(auto &e : graph[idx]) {\n      if(e.cap > 0 && used[e.to]\
    \ != timestamp) {\n        flow_t d = find_augment_path(e.to, t, min(flow, e.cap));\n\
    \        if(d > 0) {\n          e.cap -= d;\n          graph[e.to][e.rev].cap\
    \ += d;\n          return d;\n        }\n      }\n    }\n    return 0;\n  }\n\n\
    \  flow_t max_flow(int s, int t) {\n    flow_t flow = 0;\n    for(flow_t f; (f\
    \ = find_augment_path(s, t, INF)) > 0; timestamp++) {\n      flow += f;\n    }\n\
    \    return flow;\n  }\n\n  void output() {\n    for(int i = 0; i < graph.size();\
    \ i++) {\n      for(auto &e : graph[i]) {\n        if(e.isrev) continue;\n   \
    \     auto &rev_e = graph[e.to][e.rev];\n        cout << i << \"->\" << e.to <<\
    \ \" (flow: \" << rev_e.cap << \"/\" << e.cap + rev_e.cap << \")\" << endl;\n\
    \      }\n    }\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/flow/ford-fulkerson.cpp
  requiredBy: []
  timestamp: '2020-08-20 17:25:40+09:00'
  verificationStatus: LIBRARY_ALL_WA
  verifiedWith:
  - test/verify/aoj-grl-6-a-2.test.cpp
documentation_of: graph/flow/ford-fulkerson.cpp
layout: document
redirect_from:
- /library/graph/flow/ford-fulkerson.cpp
- /library/graph/flow/ford-fulkerson.cpp.html
title: "Ford-Fulkerson(\u6700\u5927\u6D41)"
---
## 概要

最大流を求めるアルゴリズム.

DFS により増加パスがとれなくなるまでフローを流すことを繰り返し, 流せなくなったら終了する.

## 使い方

* `FordFulkerson(V)`: 頂点数 `V` で初期化する.
* `add_edge(from, to, cap, idx = -1)`: 頂点 `from` から `to` に容量 `cap` の辺を追加する.
* `max_flow(s, t)`: 頂点 `s` から `t` に最大流を流し, その流量を返す.

## 計算量

$O(FE)$

$F$ は最大流
