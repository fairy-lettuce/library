---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-1254.test.cpp
    title: test/verify/aoj-1254.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-chromatic-number.test.cpp
    title: test/verify/yosupo-chromatic-number.test.cpp
  _isVerificationFailed: false
  _pathExtension: hpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/chromatic-number.md
    document_title: "Chromatic Number(\u5F69\u8272\u6570)"
    links:
    - https://www.slideshare.net/wata_orz/ss-12131479
  bundledCode: "#line 2 \"graph/others/chromatic-number.hpp\"\n\n/**\n * @brief Chromatic\
    \ Number(\u5F69\u8272\u6570)\n * @docs docs/chromatic-number.md\n * @see https://www.slideshare.net/wata_orz/ss-12131479\n\
    \ */\ntemplate< typename Matrix >\nint chromatic_number(Matrix &g) {\n  int N\
    \ = (int) g.size();\n  vector< int > es(N);\n  for(int i = 0; i < (int) g.size();\
    \ i++) {\n    for(int j = 0; j < (int) g.size(); j++) {\n      if(g[i][j] != 0)\
    \ es[i] |= 1 << j;\n    }\n  }\n  vector< int > ind(1 << N);\n  ind[0] = 1;\n\
    \  for(int S = 1; S < (1 << N); S++) {\n    int u = __builtin_ctz(S);\n    ind[S]\
    \ = ind[S ^ (1 << u)] + ind[(S ^ (1 << u)) & ~es[u]];\n  }\n  vector< int > cnt((1\
    \ << N) + 1);\n  for(int i = 0; i < (1 << N); i++) {\n    cnt[ind[i]] += __builtin_parity(i)\
    \ ? -1 : 1;\n  }\n  vector< pair< unsigned, int > > hist;\n  for(int i = 1; i\
    \ <= (1 << N); i++) {\n    if(cnt[i]) hist.emplace_back(i, cnt[i]);\n  }\n  constexpr\
    \ int mods[] = {1000000007, 1000000011, 1000000021};\n  int ret = N;\n  for(int\
    \ k = 0; k < 3; k++) {\n    auto buf = hist;\n    for(int c = 1; c < ret; c++)\
    \ {\n      int64_t sum = 0;\n      for(auto&[i, x] : buf) {\n        sum += (x\
    \ = int64_t(x) * i % mods[k]);\n      }\n      if(sum % mods[k]) ret = c;\n  \
    \  }\n  }\n  return ret;\n}\n"
  code: "#pragma once\n\n/**\n * @brief Chromatic Number(\u5F69\u8272\u6570)\n * @docs\
    \ docs/chromatic-number.md\n * @see https://www.slideshare.net/wata_orz/ss-12131479\n\
    \ */\ntemplate< typename Matrix >\nint chromatic_number(Matrix &g) {\n  int N\
    \ = (int) g.size();\n  vector< int > es(N);\n  for(int i = 0; i < (int) g.size();\
    \ i++) {\n    for(int j = 0; j < (int) g.size(); j++) {\n      if(g[i][j] != 0)\
    \ es[i] |= 1 << j;\n    }\n  }\n  vector< int > ind(1 << N);\n  ind[0] = 1;\n\
    \  for(int S = 1; S < (1 << N); S++) {\n    int u = __builtin_ctz(S);\n    ind[S]\
    \ = ind[S ^ (1 << u)] + ind[(S ^ (1 << u)) & ~es[u]];\n  }\n  vector< int > cnt((1\
    \ << N) + 1);\n  for(int i = 0; i < (1 << N); i++) {\n    cnt[ind[i]] += __builtin_parity(i)\
    \ ? -1 : 1;\n  }\n  vector< pair< unsigned, int > > hist;\n  for(int i = 1; i\
    \ <= (1 << N); i++) {\n    if(cnt[i]) hist.emplace_back(i, cnt[i]);\n  }\n  constexpr\
    \ int mods[] = {1000000007, 1000000011, 1000000021};\n  int ret = N;\n  for(int\
    \ k = 0; k < 3; k++) {\n    auto buf = hist;\n    for(int c = 1; c < ret; c++)\
    \ {\n      int64_t sum = 0;\n      for(auto&[i, x] : buf) {\n        sum += (x\
    \ = int64_t(x) * i % mods[k]);\n      }\n      if(sum % mods[k]) ret = c;\n  \
    \  }\n  }\n  return ret;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/others/chromatic-number.hpp
  requiredBy: []
  timestamp: '2021-07-21 02:10:43+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-1254.test.cpp
  - test/verify/yosupo-chromatic-number.test.cpp
documentation_of: graph/others/chromatic-number.hpp
layout: document
redirect_from:
- /library/graph/others/chromatic-number.hpp
- /library/graph/others/chromatic-number.hpp.html
title: "Chromatic Number(\u5F69\u8272\u6570)"
---
## 概要

グラフの彩色数を求める. 彩色数とは, 隣接する頂点が異なる色となるように彩色するために必要な最小色数である.

あるグラフが $k$ 彩色可能であることと, $k$ 個の独立集合で被覆できることは必要十分条件である. つまり独立集合から $k$ 個の頂点を選んで被覆する方法の総数が求まれば良い. これはbit DPと包除原理を用いて効率的に求められる.

## 使い方

* `chromatic_number(g)`: 隣接行列 `g` で表されるグラフの彩色数を求める.

## 計算量

* $O(2^N N)$
