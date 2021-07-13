---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-dpl-5-j.test.cpp
    title: test/verify/aoj-dpl-5-j.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/partition-table.md
    document_title: "Partition Table(\u5206\u5272\u6570\u30C6\u30FC\u30D6\u30EB)"
    links: []
  bundledCode: "#line 1 \"math/combinatorics/partition-table.cpp\"\n/**\n * @brief\
    \ Partition Table(\u5206\u5272\u6570\u30C6\u30FC\u30D6\u30EB)\n * @docs docs/partition-table.md\n\
    \ */\ntemplate< typename T >\nvector< vector< T > > partition_table(int n, int\
    \ k) {\n  vector< vector< T > > dp(n + 1, vector< T >(k + 1));\n  dp[0][0] = 1;\n\
    \  for(int i = 0; i <= n; i++) {\n    for(int j = 1; j <= k; j++) {\n      if(i\
    \ - j >= 0) dp[i][j] = dp[i][j - 1] + dp[i - j][j];\n      else dp[i][j] = dp[i][j\
    \ - 1];\n    }\n  }\n  return dp;\n}\n"
  code: "/**\n * @brief Partition Table(\u5206\u5272\u6570\u30C6\u30FC\u30D6\u30EB\
    )\n * @docs docs/partition-table.md\n */\ntemplate< typename T >\nvector< vector<\
    \ T > > partition_table(int n, int k) {\n  vector< vector< T > > dp(n + 1, vector<\
    \ T >(k + 1));\n  dp[0][0] = 1;\n  for(int i = 0; i <= n; i++) {\n    for(int\
    \ j = 1; j <= k; j++) {\n      if(i - j >= 0) dp[i][j] = dp[i][j - 1] + dp[i -\
    \ j][j];\n      else dp[i][j] = dp[i][j - 1];\n    }\n  }\n  return dp;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/combinatorics/partition-table.cpp
  requiredBy: []
  timestamp: '2021-07-13 21:04:36+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-dpl-5-j.test.cpp
documentation_of: math/combinatorics/partition-table.cpp
layout: document
redirect_from:
- /library/math/combinatorics/partition-table.cpp
- /library/math/combinatorics/partition-table.cpp.html
title: "Partition Table(\u5206\u5272\u6570\u30C6\u30FC\u30D6\u30EB)"
---
## 概要

分割数 $P(n, k)$ は整数 $n$ をちょうど $k$ 個の非負整数の和で表す方法の数を与える. 順序が異なるものは同一視する.

* `partition_table(n, k)`: 各 $i \leq n, j \leq k$ に対し分割数 $P(n, k)$ を求める.

## 計算量

* $O(nk)$
