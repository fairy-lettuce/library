---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':x:'
    path: test/verify/aoj-grl-6-b.test.cpp
    title: test/verify/aoj-grl-6-b.test.cpp
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes:
    links: []
  bundledCode: "#line 1 \"graph/flow/primal-dual.cpp\"\ntemplate< typename flow_t,\
    \ typename cost_t >\nstruct PrimalDual {\n  const cost_t INF;\n\n  struct edge\
    \ {\n    int to;\n    flow_t cap;\n    cost_t cost;\n    int rev;\n    bool isrev;\n\
    \  };\n  vector< vector< edge > > graph;\n  vector< cost_t > potential, min_cost;\n\
    \  vector< int > prevv, preve;\n\n  PrimalDual(int V) : graph(V), INF(numeric_limits<\
    \ cost_t >::max()) {}\n\n  void add_edge(int from, int to, flow_t cap, cost_t\
    \ cost) {\n    graph[from].emplace_back((edge) {to, cap, cost, (int) graph[to].size(),\
    \ false});\n    graph[to].emplace_back((edge) {from, 0, -cost, (int) graph[from].size()\
    \ - 1, true});\n  }\n\n  cost_t min_cost_flow(int s, int t, flow_t f) {\n    int\
    \ V = (int) graph.size();\n    cost_t ret = 0;\n    using Pi = pair< cost_t, int\
    \ >;\n    priority_queue< Pi, vector< Pi >, greater< Pi > > que;\n    potential.assign(V,\
    \ 0);\n    preve.assign(V, -1);\n    prevv.assign(V, -1);\n\n    while(f > 0)\
    \ {\n      min_cost.assign(V, INF);\n      que.emplace(0, s);\n      min_cost[s]\
    \ = 0;\n      while(!que.empty()) {\n        Pi p = que.top();\n        que.pop();\n\
    \        if(min_cost[p.second] < p.first) continue;\n        for(int i = 0; i\
    \ < graph[p.second].size(); i++) {\n          edge &e = graph[p.second][i];\n\
    \          cost_t nextCost = min_cost[p.second] + e.cost + potential[p.second]\
    \ - potential[e.to];\n          if(e.cap > 0 && min_cost[e.to] > nextCost) {\n\
    \            min_cost[e.to] = nextCost;\n            prevv[e.to] = p.second, preve[e.to]\
    \ = i;\n            que.emplace(min_cost[e.to], e.to);\n          }\n        }\n\
    \      }\n      if(min_cost[t] == INF) return -1;\n      for(int v = 0; v < V;\
    \ v++) potential[v] += min_cost[v];\n      flow_t addflow = f;\n      for(int\
    \ v = t; v != s; v = prevv[v]) {\n        addflow = min(addflow, graph[prevv[v]][preve[v]].cap);\n\
    \      }\n      f -= addflow;\n      ret += addflow * potential[t];\n      for(int\
    \ v = t; v != s; v = prevv[v]) {\n        edge &e = graph[prevv[v]][preve[v]];\n\
    \        e.cap -= addflow;\n        graph[v][e.rev].cap += addflow;\n      }\n\
    \    }\n    return ret;\n  }\n\n  void output() {\n    for(int i = 0; i < graph.size();\
    \ i++) {\n      for(auto &e : graph[i]) {\n        if(e.isrev) continue;\n   \
    \     auto &rev_e = graph[e.to][e.rev];\n        cout << i << \"->\" << e.to <<\
    \ \" (flow: \" << rev_e.cap << \"/\" << rev_e.cap + e.cap << \")\" << endl;\n\
    \      }\n    }\n  }\n};\n"
  code: "template< typename flow_t, typename cost_t >\nstruct PrimalDual {\n  const\
    \ cost_t INF;\n\n  struct edge {\n    int to;\n    flow_t cap;\n    cost_t cost;\n\
    \    int rev;\n    bool isrev;\n  };\n  vector< vector< edge > > graph;\n  vector<\
    \ cost_t > potential, min_cost;\n  vector< int > prevv, preve;\n\n  PrimalDual(int\
    \ V) : graph(V), INF(numeric_limits< cost_t >::max()) {}\n\n  void add_edge(int\
    \ from, int to, flow_t cap, cost_t cost) {\n    graph[from].emplace_back((edge)\
    \ {to, cap, cost, (int) graph[to].size(), false});\n    graph[to].emplace_back((edge)\
    \ {from, 0, -cost, (int) graph[from].size() - 1, true});\n  }\n\n  cost_t min_cost_flow(int\
    \ s, int t, flow_t f) {\n    int V = (int) graph.size();\n    cost_t ret = 0;\n\
    \    using Pi = pair< cost_t, int >;\n    priority_queue< Pi, vector< Pi >, greater<\
    \ Pi > > que;\n    potential.assign(V, 0);\n    preve.assign(V, -1);\n    prevv.assign(V,\
    \ -1);\n\n    while(f > 0) {\n      min_cost.assign(V, INF);\n      que.emplace(0,\
    \ s);\n      min_cost[s] = 0;\n      while(!que.empty()) {\n        Pi p = que.top();\n\
    \        que.pop();\n        if(min_cost[p.second] < p.first) continue;\n    \
    \    for(int i = 0; i < graph[p.second].size(); i++) {\n          edge &e = graph[p.second][i];\n\
    \          cost_t nextCost = min_cost[p.second] + e.cost + potential[p.second]\
    \ - potential[e.to];\n          if(e.cap > 0 && min_cost[e.to] > nextCost) {\n\
    \            min_cost[e.to] = nextCost;\n            prevv[e.to] = p.second, preve[e.to]\
    \ = i;\n            que.emplace(min_cost[e.to], e.to);\n          }\n        }\n\
    \      }\n      if(min_cost[t] == INF) return -1;\n      for(int v = 0; v < V;\
    \ v++) potential[v] += min_cost[v];\n      flow_t addflow = f;\n      for(int\
    \ v = t; v != s; v = prevv[v]) {\n        addflow = min(addflow, graph[prevv[v]][preve[v]].cap);\n\
    \      }\n      f -= addflow;\n      ret += addflow * potential[t];\n      for(int\
    \ v = t; v != s; v = prevv[v]) {\n        edge &e = graph[prevv[v]][preve[v]];\n\
    \        e.cap -= addflow;\n        graph[v][e.rev].cap += addflow;\n      }\n\
    \    }\n    return ret;\n  }\n\n  void output() {\n    for(int i = 0; i < graph.size();\
    \ i++) {\n      for(auto &e : graph[i]) {\n        if(e.isrev) continue;\n   \
    \     auto &rev_e = graph[e.to][e.rev];\n        cout << i << \"->\" << e.to <<\
    \ \" (flow: \" << rev_e.cap << \"/\" << rev_e.cap + e.cap << \")\" << endl;\n\
    \      }\n    }\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/flow/primal-dual.cpp
  requiredBy: []
  timestamp: '2019-11-30 23:02:43+09:00'
  verificationStatus: LIBRARY_ALL_WA
  verifiedWith:
  - test/verify/aoj-grl-6-b.test.cpp
documentation_of: graph/flow/primal-dual.cpp
layout: document
redirect_from:
- /library/graph/flow/primal-dual.cpp
- /library/graph/flow/primal-dual.cpp.html
title: graph/flow/primal-dual.cpp
---
