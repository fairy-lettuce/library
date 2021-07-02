---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 1 \"math/fps/stirling-second-kth-column.cpp\"\ntemplate< template<\
    \ typename > class FPS, typename Mint >\nFPS< Mint > stirling_second_kth_column(int\
    \ N, int K) {\n  FPS< Mint > poly(N + 1), ret(N + 1);\n  poly[1] = 1;\n  poly\
    \ = poly.exp();\n  poly[0] -= 1;\n  poly = poly.pow(K);\n  Mint rev = 1, mul =\
    \ 1;\n  for(int i = 2; i <= K; i++) rev *= i;\n  rev = Mint(1) / rev;\n  poly\
    \ *= rev;\n  for(int i = 0; i <= N; i++) {\n    ret[i] = poly[i] * mul;\n    mul\
    \ *= i + 1;\n  }\n  return ret;\n}\n"
  code: "template< template< typename > class FPS, typename Mint >\nFPS< Mint > stirling_second_kth_column(int\
    \ N, int K) {\n  FPS< Mint > poly(N + 1), ret(N + 1);\n  poly[1] = 1;\n  poly\
    \ = poly.exp();\n  poly[0] -= 1;\n  poly = poly.pow(K);\n  Mint rev = 1, mul =\
    \ 1;\n  for(int i = 2; i <= K; i++) rev *= i;\n  rev = Mint(1) / rev;\n  poly\
    \ *= rev;\n  for(int i = 0; i <= N; i++) {\n    ret[i] = poly[i] * mul;\n    mul\
    \ *= i + 1;\n  }\n  return ret;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fps/stirling-second-kth-column.cpp
  requiredBy: []
  timestamp: '2021-07-03 01:30:39+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: math/fps/stirling-second-kth-column.cpp
layout: document
redirect_from:
- /library/math/fps/stirling-second-kth-column.cpp
- /library/math/fps/stirling-second-kth-column.cpp.html
title: math/fps/stirling-second-kth-column.cpp
---
