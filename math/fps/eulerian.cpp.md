---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    document_title: "Eulerian(\u30AA\u30A4\u30E9\u30FC\u6570)"
    links: []
  bundledCode: "#line 1 \"math/fps/eulerian.cpp\"\n/**\n * @brief Eulerian(\u30AA\u30A4\
    \u30E9\u30FC\u6570)\n */\ntemplate< template< typename > class FPS, typename Mint\
    \ >\nFPS< Mint > eulerian(int N) {\n  vector< Mint > fact(N + 2), rfact(N + 2);\n\
    \  fact[0] = rfact[N + 1] = 1;\n  for(int i = 1; i <= N + 1; i++) fact[i] = fact[i\
    \ - 1] * Mint(i);\n  rfact[N + 1] /= fact[N + 1];\n  for(int i = N; i >= 0; i--)\
    \ rfact[i] = rfact[i + 1] * Mint(i + 1);\n  FPS< Mint > A(N + 1), B(N + 1);\n\
    \  for(int i = 0; i <= N; i++) {\n    A[i] = fact[N + 1] * rfact[i] * rfact[N\
    \ + 1 - i];\n    if(i & 1) A[i] *= -1;\n    B[i] = Mint(i + 1).pow(N);\n  }\n\
    \  return (A * B).pre(N + 1);\n}\n"
  code: "/**\n * @brief Eulerian(\u30AA\u30A4\u30E9\u30FC\u6570)\n */\ntemplate< template<\
    \ typename > class FPS, typename Mint >\nFPS< Mint > eulerian(int N) {\n  vector<\
    \ Mint > fact(N + 2), rfact(N + 2);\n  fact[0] = rfact[N + 1] = 1;\n  for(int\
    \ i = 1; i <= N + 1; i++) fact[i] = fact[i - 1] * Mint(i);\n  rfact[N + 1] /=\
    \ fact[N + 1];\n  for(int i = N; i >= 0; i--) rfact[i] = rfact[i + 1] * Mint(i\
    \ + 1);\n  FPS< Mint > A(N + 1), B(N + 1);\n  for(int i = 0; i <= N; i++) {\n\
    \    A[i] = fact[N + 1] * rfact[i] * rfact[N + 1 - i];\n    if(i & 1) A[i] *=\
    \ -1;\n    B[i] = Mint(i + 1).pow(N);\n  }\n  return (A * B).pre(N + 1);\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fps/eulerian.cpp
  requiredBy: []
  timestamp: '2021-07-03 01:30:39+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: math/fps/eulerian.cpp
layout: document
redirect_from:
- /library/math/fps/eulerian.cpp
- /library/math/fps/eulerian.cpp.html
title: "Eulerian(\u30AA\u30A4\u30E9\u30FC\u6570)"
---
