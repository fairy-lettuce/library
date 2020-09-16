---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-0275.test.cpp
    title: test/verify/aoj-0275.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    document_title: "Offline-Dag-Reachability(DAG\u306E\u5230\u9054\u53EF\u80FD\u6027\
      \u30AF\u30A8\u30EA)"
    links: []
  bundledCode: "#line 1 \"graph/others/offline-dag-reachability.cpp\"\n/**\n * @brief\
    \ Offline-Dag-Reachability(DAG\u306E\u5230\u9054\u53EF\u80FD\u6027\u30AF\u30A8\
    \u30EA)\n */\ntemplate< typename T >\nvector< int > offline_dag_reachability(const\
    \ Graph< T > &g, vector< pair< int, int > > &qs) {\n  const int N = (int) g.size();\n\
    \  const int Q = (int) qs.size();\n  auto ord = topological_sort(g);\n  vector<\
    \ int > ans(Q);\n  for(int l = 0; l < Q; l += 64) {\n    int r = min(Q, l + 64);\n\
    \    vector< int64_t > dp(N);\n    for(int k = l; k < r; k++) {\n      dp[qs[k].first]\
    \ |= int64_t(1) << (k - l);\n    }\n    for(auto &idx : ord) {\n      for(auto\
    \ &to : g.g[idx]) dp[to] |= dp[idx];\n    }\n    for(int k = l; k < r; k++) {\n\
    \      ans[k] = (dp[qs[k].second] >> (k - l)) & 1;\n    }\n  }\n  return ans;\n\
    }\n"
  code: "/**\n * @brief Offline-Dag-Reachability(DAG\u306E\u5230\u9054\u53EF\u80FD\
    \u6027\u30AF\u30A8\u30EA)\n */\ntemplate< typename T >\nvector< int > offline_dag_reachability(const\
    \ Graph< T > &g, vector< pair< int, int > > &qs) {\n  const int N = (int) g.size();\n\
    \  const int Q = (int) qs.size();\n  auto ord = topological_sort(g);\n  vector<\
    \ int > ans(Q);\n  for(int l = 0; l < Q; l += 64) {\n    int r = min(Q, l + 64);\n\
    \    vector< int64_t > dp(N);\n    for(int k = l; k < r; k++) {\n      dp[qs[k].first]\
    \ |= int64_t(1) << (k - l);\n    }\n    for(auto &idx : ord) {\n      for(auto\
    \ &to : g.g[idx]) dp[to] |= dp[idx];\n    }\n    for(int k = l; k < r; k++) {\n\
    \      ans[k] = (dp[qs[k].second] >> (k - l)) & 1;\n    }\n  }\n  return ans;\n\
    }\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/others/offline-dag-reachability.cpp
  requiredBy: []
  timestamp: '2020-03-26 01:02:16+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-0275.test.cpp
documentation_of: graph/others/offline-dag-reachability.cpp
layout: document
redirect_from:
- /library/graph/others/offline-dag-reachability.cpp
- /library/graph/others/offline-dag-reachability.cpp.html
title: "Offline-Dag-Reachability(DAG\u306E\u5230\u9054\u53EF\u80FD\u6027\u30AF\u30A8\
  \u30EA)"
---
