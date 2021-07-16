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
    \  if(N <= 0) return {Mint(1)};\n  auto f = stirling_first< FPS, Mint >(N >> 1);\n\
    \  f *= f.taylor_shift(-(N >> 1));\n  if(N & 1) f = (f << 1) - f * (N - 1);\n\
    \  return f;\n}\n"
  code: "/**\n * @brief Stirling First(\u7B2C\u4E00\u7A2E\u30B9\u30BF\u30FC\u30EA\u30F3\
    \u30B0\u6570)\n */\ntemplate< template< typename > class FPS, typename Mint >\n\
    FPS< Mint > stirling_first(int N) {\n  if(N <= 0) return {Mint(1)};\n  auto f\
    \ = stirling_first< FPS, Mint >(N >> 1);\n  f *= f.taylor_shift(-(N >> 1));\n\
    \  if(N & 1) f = (f << 1) - f * (N - 1);\n  return f;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fps/stirling-first.cpp
  requiredBy: []
  timestamp: '2021-07-17 00:28:41+09:00'
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
