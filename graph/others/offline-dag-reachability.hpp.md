---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: graph/graph-template.hpp
    title: graph/graph-template.hpp
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-0275.test.cpp
    title: test/verify/aoj-0275.test.cpp
  _isVerificationFailed: false
  _pathExtension: hpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/offline-dag-reachability.md
    document_title: "Offline-Dag-Reachability(DAG\u306E\u5230\u9054\u53EF\u80FD\u6027\
      \u30AF\u30A8\u30EA)"
    links: []
  bundledCode: "#line 2 \"graph/others/offline-dag-reachability.hpp\"\n\n#line 2 \"\
    graph/graph-template.hpp\"\n\ntemplate< typename T = int >\nstruct Edge {\n  int\
    \ from, to;\n  T cost;\n  int idx;\n\n  Edge() = default;\n\n  Edge(int from,\
    \ int to, T cost = 1, int idx = -1) : from(from), to(to), cost(cost), idx(idx)\
    \ {}\n\n  operator int() const { return to; }\n};\n\ntemplate< typename T = int\
    \ >\nstruct Graph {\n  vector< vector< Edge< T > > > g;\n  int es;\n\n  Graph()\
    \ = default;\n\n  explicit Graph(int n) : g(n), es(0) {}\n\n  size_t size() const\
    \ {\n    return g.size();\n  }\n\n  void add_directed_edge(int from, int to, T\
    \ cost = 1) {\n    g[from].emplace_back(from, to, cost, es++);\n  }\n\n  void\
    \ add_edge(int from, int to, T cost = 1) {\n    g[from].emplace_back(from, to,\
    \ cost, es);\n    g[to].emplace_back(to, from, cost, es++);\n  }\n\n  void read(int\
    \ M, int padding = -1, bool weighted = false, bool directed = false) {\n    for(int\
    \ i = 0; i < M; i++) {\n      int a, b;\n      cin >> a >> b;\n      a += padding;\n\
    \      b += padding;\n      T c = T(1);\n      if(weighted) cin >> c;\n      if(directed)\
    \ add_directed_edge(a, b, c);\n      else add_edge(a, b, c);\n    }\n  }\n};\n\
    \ntemplate< typename T = int >\nusing Edges = vector< Edge< T > >;\n#line 4 \"\
    graph/others/offline-dag-reachability.hpp\"\n\n/**\n * @brief Offline-Dag-Reachability(DAG\u306E\
    \u5230\u9054\u53EF\u80FD\u6027\u30AF\u30A8\u30EA)\n * @docs docs/offline-dag-reachability.md\n\
    \ */\n\ntemplate< typename T >\nvector< int > offline_dag_reachability(const Graph<\
    \ T > &g, vector< pair< int, int > > &qs) {\n  const int N = (int) g.size();\n\
    \  const int Q = (int) qs.size();\n  auto ord = topological_sort(g);\n  vector<\
    \ int > ans(Q);\n  for(int l = 0; l < Q; l += 64) {\n    int r = min(Q, l + 64);\n\
    \    vector< int64_t > dp(N);\n    for(int k = l; k < r; k++) {\n      dp[qs[k].first]\
    \ |= int64_t(1) << (k - l);\n    }\n    for(auto &idx : ord) {\n      for(auto\
    \ &to : g.g[idx]) dp[to] |= dp[idx];\n    }\n    for(int k = l; k < r; k++) {\n\
    \      ans[k] = (dp[qs[k].second] >> (k - l)) & 1;\n    }\n  }\n  return ans;\n\
    }\n"
  code: "#pragma once\n\n#include \"../graph-template.hpp\"\n\n/**\n * @brief Offline-Dag-Reachability(DAG\u306E\
    \u5230\u9054\u53EF\u80FD\u6027\u30AF\u30A8\u30EA)\n * @docs docs/offline-dag-reachability.md\n\
    \ */\n\ntemplate< typename T >\nvector< int > offline_dag_reachability(const Graph<\
    \ T > &g, vector< pair< int, int > > &qs) {\n  const int N = (int) g.size();\n\
    \  const int Q = (int) qs.size();\n  auto ord = topological_sort(g);\n  vector<\
    \ int > ans(Q);\n  for(int l = 0; l < Q; l += 64) {\n    int r = min(Q, l + 64);\n\
    \    vector< int64_t > dp(N);\n    for(int k = l; k < r; k++) {\n      dp[qs[k].first]\
    \ |= int64_t(1) << (k - l);\n    }\n    for(auto &idx : ord) {\n      for(auto\
    \ &to : g.g[idx]) dp[to] |= dp[idx];\n    }\n    for(int k = l; k < r; k++) {\n\
    \      ans[k] = (dp[qs[k].second] >> (k - l)) & 1;\n    }\n  }\n  return ans;\n\
    }\n"
  dependsOn:
  - graph/graph-template.hpp
  isVerificationFile: false
  path: graph/others/offline-dag-reachability.hpp
  requiredBy: []
  timestamp: '2021-07-01 02:53:34+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-0275.test.cpp
documentation_of: graph/others/offline-dag-reachability.hpp
layout: document
redirect_from:
- /library/graph/others/offline-dag-reachability.hpp
- /library/graph/others/offline-dag-reachability.hpp.html
title: "Offline-Dag-Reachability(DAG\u306E\u5230\u9054\u53EF\u80FD\u6027\u30AF\u30A8\
  \u30EA)"
---
## 概要

DAG(閉路のない有向グラフ) が与えられたとき, ある頂点からある頂点に到達できるかどうかを調べるクエリをビット並列により処理する.

## 使い方

* `offline_dag_reachability(g, qs)`: DAG `g` について, `qs` の各クエリについて頂点 `qs[i].first` から `qs[i].second` に到達できるか判定し, 到達できる場合は `1`, できない場合は `0` を格納して返す.

## 計算量

$O(\frac {(E + V) Q} {64})$
