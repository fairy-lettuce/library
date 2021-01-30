---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    _deprecated_at_docs: docs/binomial-table.md
    document_title: "Binomial-Table(\u4E8C\u9805\u4FC2\u6570\u30C6\u30FC\u30D6\u30EB\
      )"
    links: []
  bundledCode: "#line 1 \"math/combinatorics/binomial-table.cpp\"\n/**\n * @brief\
    \ Binomial-Table(\u4E8C\u9805\u4FC2\u6570\u30C6\u30FC\u30D6\u30EB)\n * @docs docs/binomial-table.md\n\
    \ */\ntemplate< typename T >\nvector< vector< T > > binomial_table(int N) {\n\
    \  vector< vector< T > > mat(N + 1, vector< T >(N + 1));\n  for(int i = 0; i <=\
    \ N; i++) {\n    for(int j = 0; j <= i; j++) {\n      if(j == 0 || j == i) mat[i][j]\
    \ = 1;\n      else mat[i][j] = mat[i - 1][j - 1] + mat[i - 1][j];\n    }\n  }\n\
    \  return mat;\n}\n"
  code: "/**\n * @brief Binomial-Table(\u4E8C\u9805\u4FC2\u6570\u30C6\u30FC\u30D6\u30EB\
    )\n * @docs docs/binomial-table.md\n */\ntemplate< typename T >\nvector< vector<\
    \ T > > binomial_table(int N) {\n  vector< vector< T > > mat(N + 1, vector< T\
    \ >(N + 1));\n  for(int i = 0; i <= N; i++) {\n    for(int j = 0; j <= i; j++)\
    \ {\n      if(j == 0 || j == i) mat[i][j] = 1;\n      else mat[i][j] = mat[i -\
    \ 1][j - 1] + mat[i - 1][j];\n    }\n  }\n  return mat;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/combinatorics/binomial-table.cpp
  requiredBy: []
  timestamp: '2020-02-24 19:08:02+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: math/combinatorics/binomial-table.cpp
layout: document
redirect_from:
- /library/math/combinatorics/binomial-table.cpp
- /library/math/combinatorics/binomial-table.cpp.html
title: "Binomial-Table(\u4E8C\u9805\u4FC2\u6570\u30C6\u30FC\u30D6\u30EB)"
---
## 概要

二項係数テーブルをパスカルの三角形より求める.

* `binomial_table(n)`: `n` 以下の二項係数テーブルを返す.

## 計算量

* $O(n^2)$
