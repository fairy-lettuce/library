---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-dpl-1-e.test.cpp
    title: test/verify/aoj-dpl-1-e.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/edit-distance.md
    document_title: "Edit Distance(\u7DE8\u96C6\u8DDD\u96E2)"
    links: []
  bundledCode: "#line 1 \"dp/edit-distance.cpp\"\n/**\n * @brief Edit Distance(\u7DE8\
    \u96C6\u8DDD\u96E2)\n * @docs docs/edit-distance.md\n */\nint edit_distance(const\
    \ string &S, const string &T) {\n  const int N = (int) S.size(), M = (int) T.size();\n\
    \  vector< vector< int > > dp(N + 1, vector< int >(M + 1, N + M));\n  for(int\
    \ i = 0; i <= N; i++) dp[i][0] = i;\n  for(int i = 0; i <= M; i++) dp[0][i] =\
    \ i;\n  for(int i = 1; i <= N; i++) {\n    for(int j = 1; j <= M; j++) {\n   \
    \   dp[i][j] = min(dp[i][j], dp[i - 1][j] + 1);\n      dp[i][j] = min(dp[i][j],\
    \ dp[i][j - 1] + 1);\n      dp[i][j] = min(dp[i][j], dp[i - 1][j - 1] + (S[i -\
    \ 1] != T[j - 1]));\n    }\n  }\n  return dp[N][M];\n}\n"
  code: "/**\n * @brief Edit Distance(\u7DE8\u96C6\u8DDD\u96E2)\n * @docs docs/edit-distance.md\n\
    \ */\nint edit_distance(const string &S, const string &T) {\n  const int N = (int)\
    \ S.size(), M = (int) T.size();\n  vector< vector< int > > dp(N + 1, vector< int\
    \ >(M + 1, N + M));\n  for(int i = 0; i <= N; i++) dp[i][0] = i;\n  for(int i\
    \ = 0; i <= M; i++) dp[0][i] = i;\n  for(int i = 1; i <= N; i++) {\n    for(int\
    \ j = 1; j <= M; j++) {\n      dp[i][j] = min(dp[i][j], dp[i - 1][j] + 1);\n \
    \     dp[i][j] = min(dp[i][j], dp[i][j - 1] + 1);\n      dp[i][j] = min(dp[i][j],\
    \ dp[i - 1][j - 1] + (S[i - 1] != T[j - 1]));\n    }\n  }\n  return dp[N][M];\n\
    }\n"
  dependsOn: []
  isVerificationFile: false
  path: dp/edit-distance.cpp
  requiredBy: []
  timestamp: '2021-07-13 19:53:12+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-dpl-1-e.test.cpp
documentation_of: dp/edit-distance.cpp
layout: document
redirect_from:
- /library/dp/edit-distance.cpp
- /library/dp/edit-distance.cpp.html
title: "Edit Distance(\u7DE8\u96C6\u8DDD\u96E2)"
---
## 概要

レーベルシュタイン距離とも呼ばれる. $2$ つの文字列がどの程度異なっているかを示す距離の一種である.

$1$ 文字の挿入・削除・置換によって, 一方の文字列をもう一方の文字列に変形するのに必要な手順の最小値として定義される.

* `edit_distance(S, T)`: 文字列 `S, T` の編集距離を返す.

## 計算量

* $O(nm)$
