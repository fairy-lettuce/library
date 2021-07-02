---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-bernoulli-number.test.cpp
    title: test/verify/yosupo-bernoulli-number.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    document_title: "Bernoulli(\u30D9\u30EB\u30CC\u30FC\u30A4\u6570)"
    links: []
  bundledCode: "#line 1 \"math/fps/bernoulli.cpp\"\n/**\n * @brief Bernoulli(\u30D9\
    \u30EB\u30CC\u30FC\u30A4\u6570)\n */\ntemplate< template< typename > class FPS,\
    \ typename Mint >\nFPS< Mint > bernoulli(int N) {\n  FPS< Mint > poly(N + 1);\n\
    \  poly[0] = Mint(1);\n  for(int i = 1; i <= N; i++) {\n    poly[i] = poly[i -\
    \ 1] / Mint(i + 1);\n  }\n  poly = poly.inv();\n  Mint tmp(1);\n  for(int i =\
    \ 1; i <= N; i++) {\n    tmp *= Mint(i);\n    poly[i] *= tmp;\n  }\n  return poly;\n\
    }\n"
  code: "/**\n * @brief Bernoulli(\u30D9\u30EB\u30CC\u30FC\u30A4\u6570)\n */\ntemplate<\
    \ template< typename > class FPS, typename Mint >\nFPS< Mint > bernoulli(int N)\
    \ {\n  FPS< Mint > poly(N + 1);\n  poly[0] = Mint(1);\n  for(int i = 1; i <= N;\
    \ i++) {\n    poly[i] = poly[i - 1] / Mint(i + 1);\n  }\n  poly = poly.inv();\n\
    \  Mint tmp(1);\n  for(int i = 1; i <= N; i++) {\n    tmp *= Mint(i);\n    poly[i]\
    \ *= tmp;\n  }\n  return poly;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fps/bernoulli.cpp
  requiredBy: []
  timestamp: '2021-07-03 01:30:39+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-bernoulli-number.test.cpp
documentation_of: math/fps/bernoulli.cpp
layout: document
redirect_from:
- /library/math/fps/bernoulli.cpp
- /library/math/fps/bernoulli.cpp.html
title: "Bernoulli(\u30D9\u30EB\u30CC\u30FC\u30A4\u6570)"
---
