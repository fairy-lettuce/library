---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':x:'
    path: test/verify/aoj-dpl-1-f.test.cpp
    title: test/verify/aoj-dpl-1-f.test.cpp
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes:
    _deprecated_at_docs: docs/knapsack-01-2.md
    document_title: "Knapsack-01(0-1\u30CA\u30C3\u30D7\u30B5\u30C3\u30AF\u554F\u984C\
      ) $O(N \\sum {v_i})$"
    links: []
  bundledCode: "#line 1 \"dp/knapsack-01-2.cpp\"\n/**\n * @brief Knapsack-01(0-1\u30CA\
    \u30C3\u30D7\u30B5\u30C3\u30AF\u554F\u984C) $O(N \\sum {v_i})$\n * @docs docs/knapsack-01-2.md\n\
    \ */\ntemplate< typename T >\nT knapsack_01_2(const vector< T > &w, const vector<\
    \ int > &v, const T &W) {\n  const int N = (int) w.size();\n  const int sum =\
    \ accumulate(begin(v), end(v), 0);\n  vector< T > dp(sum + 1, W + 1);\n  dp[0]\
    \ = T();\n  for(int i = 0; i < N; i++) {\n    for(int j = sum; j >= v[i]; j--)\
    \ {\n      dp[j] = min(dp[j], dp[j - v[i]] + w[i]);\n    }\n  }\n  int ret = 0;\n\
    \  for(int i = 0; i <= sum; i++) {\n    if(dp[i] <= W) ret = i;\n  }\n  return\
    \ ret;\n}\n"
  code: "/**\n * @brief Knapsack-01(0-1\u30CA\u30C3\u30D7\u30B5\u30C3\u30AF\u554F\u984C\
    ) $O(N \\sum {v_i})$\n * @docs docs/knapsack-01-2.md\n */\ntemplate< typename\
    \ T >\nT knapsack_01_2(const vector< T > &w, const vector< int > &v, const T &W)\
    \ {\n  const int N = (int) w.size();\n  const int sum = accumulate(begin(v), end(v),\
    \ 0);\n  vector< T > dp(sum + 1, W + 1);\n  dp[0] = T();\n  for(int i = 0; i <\
    \ N; i++) {\n    for(int j = sum; j >= v[i]; j--) {\n      dp[j] = min(dp[j],\
    \ dp[j - v[i]] + w[i]);\n    }\n  }\n  int ret = 0;\n  for(int i = 0; i <= sum;\
    \ i++) {\n    if(dp[i] <= W) ret = i;\n  }\n  return ret;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: dp/knapsack-01-2.cpp
  requiredBy: []
  timestamp: '2020-02-21 17:07:30+09:00'
  verificationStatus: LIBRARY_ALL_WA
  verifiedWith:
  - test/verify/aoj-dpl-1-f.test.cpp
documentation_of: dp/knapsack-01-2.cpp
layout: document
redirect_from:
- /library/dp/knapsack-01-2.cpp
- /library/dp/knapsack-01-2.cpp.html
title: "Knapsack-01(0-1\u30CA\u30C3\u30D7\u30B5\u30C3\u30AF\u554F\u984C) $O(N \\sum\
  \ {v_i})$"
---
## 概要

0-1 ナップサック問題を次に示す.

重さ $w_i$, 価値 $v_i$ であるような $N$ 個の品物がある. 重さの和が $W$ 以下となるように選ぶとき, 価値の最大値を求めよ.

* `knapsack_01_2(w, v, W)`: 重さが `W` 以下で価値の和の最大値を返す.

## 計算量

* $O(N \sum {v_i})$
