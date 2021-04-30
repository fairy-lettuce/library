---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-1615.test.cpp
    title: test/verify/aoj-1615.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links: []
  bundledCode: "#line 1 \"graph/flow/maxflow-lower-bound.cpp\"\ntemplate< typename\
    \ flow_t, template< typename > class F >\nstruct MaxFlowLowerBound {\n  F< flow_t\
    \ > flow;\n  vector< flow_t > in, up;\n  typename F< flow_t >::edge *latte, *malta;\n\
    \  int X, Y, V;\n  flow_t sum;\n\n  MaxFlowLowerBound(int V) : V(V), flow(V +\
    \ 2), X(V), Y(V + 1), sum(0), in(V) {}\n\n  void add_edge(int from, int to, flow_t\
    \ low, flow_t high) {\n    assert(from != to);\n    flow.add_edge(from, to, high\
    \ - low, up.size());\n    in[from] -= low;\n    in[to] += low;\n    up.emplace_back(high);\n\
    \  }\n\n  void build() {\n    for(int i = 0; i < V; i++) {\n      if(in[i] > 0)\
    \ {\n        flow.add_edge(X, i, in[i]);\n        sum += in[i];\n      } else\
    \ if(in[i] < 0) {\n        flow.add_edge(i, Y, -in[i]);\n      }\n    }\n  }\n\
    \n  bool can_flow(int s, int t) {\n    assert(s != t);\n    flow.add_edge(t, s,\
    \ flow.INF);\n    latte = &flow.graph[t].back();\n    malta = &flow.graph[s].back();\n\
    \    return can_flow();\n  }\n\n  bool can_flow() {\n    build();\n    auto ret\
    \ = flow.max_flow(X, Y);\n    return ret >= sum;\n  }\n\n  flow_t max_flow(int\
    \ s, int t) {\n    if(can_flow(s, t)) {\n      return flow.max_flow(s, t);\n \
    \   } else {\n      return -1;\n    }\n  }\n\n  flow_t min_flow(int s, int t)\
    \ {\n    if(can_flow(s, t)) {\n      auto ret = flow.INF - latte->cap;\n     \
    \ latte->cap = malta->cap = 0;\n      return ret - flow.max_flow(t, s);\n    }\
    \ else {\n      return -1;\n    }\n  }\n\n  void output(int M) {\n    vector<\
    \ flow_t > ans(M);\n    for(int i = 0; i < flow.graph.size(); i++) {\n      for(auto\
    \ &e : flow.graph[i]) {\n        if(!e.isrev && ~e.idx) ans[e.idx] = up[e.idx]\
    \ - e.cap;\n      }\n    }\n    for(auto &p : ans) cout << p << endl;\n  }\n};\n"
  code: "template< typename flow_t, template< typename > class F >\nstruct MaxFlowLowerBound\
    \ {\n  F< flow_t > flow;\n  vector< flow_t > in, up;\n  typename F< flow_t >::edge\
    \ *latte, *malta;\n  int X, Y, V;\n  flow_t sum;\n\n  MaxFlowLowerBound(int V)\
    \ : V(V), flow(V + 2), X(V), Y(V + 1), sum(0), in(V) {}\n\n  void add_edge(int\
    \ from, int to, flow_t low, flow_t high) {\n    assert(from != to);\n    flow.add_edge(from,\
    \ to, high - low, up.size());\n    in[from] -= low;\n    in[to] += low;\n    up.emplace_back(high);\n\
    \  }\n\n  void build() {\n    for(int i = 0; i < V; i++) {\n      if(in[i] > 0)\
    \ {\n        flow.add_edge(X, i, in[i]);\n        sum += in[i];\n      } else\
    \ if(in[i] < 0) {\n        flow.add_edge(i, Y, -in[i]);\n      }\n    }\n  }\n\
    \n  bool can_flow(int s, int t) {\n    assert(s != t);\n    flow.add_edge(t, s,\
    \ flow.INF);\n    latte = &flow.graph[t].back();\n    malta = &flow.graph[s].back();\n\
    \    return can_flow();\n  }\n\n  bool can_flow() {\n    build();\n    auto ret\
    \ = flow.max_flow(X, Y);\n    return ret >= sum;\n  }\n\n  flow_t max_flow(int\
    \ s, int t) {\n    if(can_flow(s, t)) {\n      return flow.max_flow(s, t);\n \
    \   } else {\n      return -1;\n    }\n  }\n\n  flow_t min_flow(int s, int t)\
    \ {\n    if(can_flow(s, t)) {\n      auto ret = flow.INF - latte->cap;\n     \
    \ latte->cap = malta->cap = 0;\n      return ret - flow.max_flow(t, s);\n    }\
    \ else {\n      return -1;\n    }\n  }\n\n  void output(int M) {\n    vector<\
    \ flow_t > ans(M);\n    for(int i = 0; i < flow.graph.size(); i++) {\n      for(auto\
    \ &e : flow.graph[i]) {\n        if(!e.isrev && ~e.idx) ans[e.idx] = up[e.idx]\
    \ - e.cap;\n      }\n    }\n    for(auto &p : ans) cout << p << endl;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/flow/maxflow-lower-bound.cpp
  requiredBy: []
  timestamp: '2019-11-30 23:02:43+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-1615.test.cpp
documentation_of: graph/flow/maxflow-lower-bound.cpp
layout: document
redirect_from:
- /library/graph/flow/maxflow-lower-bound.cpp
- /library/graph/flow/maxflow-lower-bound.cpp.html
title: graph/flow/maxflow-lower-bound.cpp
---
