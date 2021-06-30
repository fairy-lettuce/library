---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-1254.test.cpp
    title: test/verify/aoj-1254.test.cpp
  _isVerificationFailed: false
  _pathExtension: hpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/chromatic-number.md
    document_title: "Chromatic-Number(\u5F69\u8272\u6570)"
    links:
    - https://www.slideshare.net/wata_orz/ss-12131479
  bundledCode: "#line 2 \"graph/others/chromatic-number.hpp\"\n/**\n * @brief Chromatic-Number(\u5F69\
    \u8272\u6570)\n * @docs docs/chromatic-number.md\n * @see https://www.slideshare.net/wata_orz/ss-12131479\n\
    \ */\ntemplate< typename Matrix >\nint chromatic_number(Matrix &g) {\n  int N\
    \ = (int) g.size();\n  vector< int > es(N);\n  for(int i = 0; i < (int)g.size();\
    \ i++) {\n    for(int j = 0; j < (int)g.size(); j++) {\n      if(g[i][j] != 0)\
    \ es[i] |= 1 << j;\n    }\n  }\n  int ret = N;\n  for(int d : {7, 11, 21}) {\n\
    \    int mod = 1e9 + d;\n    vector< int > ind(1 << N), aux(1 << N, 1);\n    ind[0]\
    \ = 1;\n    for(int S = 1; S < 1 << N; S++) {\n      int u = __builtin_ctz(S);\n\
    \      ind[S] = ind[S ^ (1 << u)] + ind[(S ^ (1 << u)) & ~es[u]];\n    }\n   \
    \ for(int i = 1; i < ret; i++) {\n      int64_t all = 0;\n      for(int j = 0;\
    \ j < 1 << N; j++) {\n        int S = j ^(j >> 1);\n        aux[S] = (1LL * aux[S]\
    \ * ind[S]) % mod;\n        all += j & 1 ? aux[S] : mod - aux[S];\n      }\n \
    \     if(all % mod) ret = i;\n    }\n  }\n  return ret;\n}\n"
  code: "#pragma once\n/**\n * @brief Chromatic-Number(\u5F69\u8272\u6570)\n * @docs\
    \ docs/chromatic-number.md\n * @see https://www.slideshare.net/wata_orz/ss-12131479\n\
    \ */\ntemplate< typename Matrix >\nint chromatic_number(Matrix &g) {\n  int N\
    \ = (int) g.size();\n  vector< int > es(N);\n  for(int i = 0; i < (int)g.size();\
    \ i++) {\n    for(int j = 0; j < (int)g.size(); j++) {\n      if(g[i][j] != 0)\
    \ es[i] |= 1 << j;\n    }\n  }\n  int ret = N;\n  for(int d : {7, 11, 21}) {\n\
    \    int mod = 1e9 + d;\n    vector< int > ind(1 << N), aux(1 << N, 1);\n    ind[0]\
    \ = 1;\n    for(int S = 1; S < 1 << N; S++) {\n      int u = __builtin_ctz(S);\n\
    \      ind[S] = ind[S ^ (1 << u)] + ind[(S ^ (1 << u)) & ~es[u]];\n    }\n   \
    \ for(int i = 1; i < ret; i++) {\n      int64_t all = 0;\n      for(int j = 0;\
    \ j < 1 << N; j++) {\n        int S = j ^(j >> 1);\n        aux[S] = (1LL * aux[S]\
    \ * ind[S]) % mod;\n        all += j & 1 ? aux[S] : mod - aux[S];\n      }\n \
    \     if(all % mod) ret = i;\n    }\n  }\n  return ret;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/others/chromatic-number.hpp
  requiredBy: []
  timestamp: '2021-07-01 02:53:34+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-1254.test.cpp
documentation_of: graph/others/chromatic-number.hpp
layout: document
redirect_from:
- /library/graph/others/chromatic-number.hpp
- /library/graph/others/chromatic-number.hpp.html
title: "Chromatic-Number(\u5F69\u8272\u6570)"
---
## 概要

グラフの彩色数を求める. 彩色数とは, 隣接する頂点が異なる色となるように彩色するために必要な最小色数である.

あるグラフが $k$ 彩色可能であることと, $k$ 個の独立集合で被覆できることは必要十分条件である. つまり独立集合から $k$ 個の頂点を選んで被覆する方法の総数が求まれば良い. これはbit DPと包除原理を用いて効率的に求められる.

## 使い方

* `chromatic_number(g)`: 隣接行列 `g` で表されるグラフの彩色数を求める.

## 計算量

* $O(2^N N)$
