---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-stirling-number-of-the-first-kind.test.cpp
    title: test/verify/yosupo-stirling-number-of-the-first-kind.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    document_title: "Stirling First(\u7B2C\u4E00\u7A2E\u30B9\u30BF\u30FC\u30EA\u30F3\
      \u30B0\u6570)"
    links: []
  bundledCode: "#line 1 \"math/fps/stirling-first.cpp\"\n/**\n * @brief Stirling First(\u7B2C\
    \u4E00\u7A2E\u30B9\u30BF\u30FC\u30EA\u30F3\u30B0\u6570)\n */\ntemplate< template<\
    \ typename > class FPS, typename Mint >\nFPS< Mint > stirling_first(int N) {\n\
    \  if(N == 0) return {Mint(1)};\n  int M = 1;\n  vector< Mint > fact(N + 1), rfact(N\
    \ + 1);\n  fact[0] = rfact[N] = Mint(1);\n  for(int i = 1; i <= N; i++) fact[i]\
    \ = fact[i - 1] * i;\n  rfact[N] /= fact[N];\n  for(int i = N - 1; i >= 0; i--)\
    \ rfact[i] = rfact[i + 1] * (i + 1);\n  FPS< Mint > ret({Mint(0), Mint(1)});\n\
    \  for(int k = 30 - __builtin_clz(N); k >= 0; k--) {\n    FPS< Mint > as(M + 1),\
    \ bs(M + 1);\n    for(int i = 0; i <= M; i++) as[i] = ret[i] * fact[i];\n    bs[M]\
    \ = Mint(1);\n    for(int i = 1; i <= M; i++) bs[M - i] = bs[M - (i - 1)] * Mint(-M);\n\
    \    for(int i = 0; i <= M; i++) bs[M - i] *= rfact[i];\n    auto cs = as * bs;\n\
    \    FPS< Mint > ds(M + 1);\n    for(int i = 0; i <= M; i++) ds[i] = rfact[i]\
    \ * cs[M + i];\n    ret *= ds;\n    M <<= 1;\n    if((N >> k) & 1) {\n      FPS<\
    \ Mint > ts(M + 1 + 1, Mint(0));\n      for(int i = 0; i <= M; i++) {\n      \
    \  ts[i + 0] -= ret[i] * Mint(M);\n        ts[i + 1] += ret[i];\n      }\n   \
    \   ret = ts;\n      M |= 1;\n    }\n  }\n  return ret;\n}\n"
  code: "/**\n * @brief Stirling First(\u7B2C\u4E00\u7A2E\u30B9\u30BF\u30FC\u30EA\u30F3\
    \u30B0\u6570)\n */\ntemplate< template< typename > class FPS, typename Mint >\n\
    FPS< Mint > stirling_first(int N) {\n  if(N == 0) return {Mint(1)};\n  int M =\
    \ 1;\n  vector< Mint > fact(N + 1), rfact(N + 1);\n  fact[0] = rfact[N] = Mint(1);\n\
    \  for(int i = 1; i <= N; i++) fact[i] = fact[i - 1] * i;\n  rfact[N] /= fact[N];\n\
    \  for(int i = N - 1; i >= 0; i--) rfact[i] = rfact[i + 1] * (i + 1);\n  FPS<\
    \ Mint > ret({Mint(0), Mint(1)});\n  for(int k = 30 - __builtin_clz(N); k >= 0;\
    \ k--) {\n    FPS< Mint > as(M + 1), bs(M + 1);\n    for(int i = 0; i <= M; i++)\
    \ as[i] = ret[i] * fact[i];\n    bs[M] = Mint(1);\n    for(int i = 1; i <= M;\
    \ i++) bs[M - i] = bs[M - (i - 1)] * Mint(-M);\n    for(int i = 0; i <= M; i++)\
    \ bs[M - i] *= rfact[i];\n    auto cs = as * bs;\n    FPS< Mint > ds(M + 1);\n\
    \    for(int i = 0; i <= M; i++) ds[i] = rfact[i] * cs[M + i];\n    ret *= ds;\n\
    \    M <<= 1;\n    if((N >> k) & 1) {\n      FPS< Mint > ts(M + 1 + 1, Mint(0));\n\
    \      for(int i = 0; i <= M; i++) {\n        ts[i + 0] -= ret[i] * Mint(M);\n\
    \        ts[i + 1] += ret[i];\n      }\n      ret = ts;\n      M |= 1;\n    }\n\
    \  }\n  return ret;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fps/stirling-first.cpp
  requiredBy: []
  timestamp: '2021-07-13 20:24:08+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-stirling-number-of-the-first-kind.test.cpp
documentation_of: math/fps/stirling-first.cpp
layout: document
redirect_from:
- /library/math/fps/stirling-first.cpp
- /library/math/fps/stirling-first.cpp.html
title: "Stirling First(\u7B2C\u4E00\u7A2E\u30B9\u30BF\u30FC\u30EA\u30F3\u30B0\u6570\
  )"
---
