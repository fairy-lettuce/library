---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    document_title: "Bell(\u30D9\u30EB\u6570)"
    links: []
  bundledCode: "#line 1 \"math/fps/bell.cpp\"\n/**\n * @brief Bell(\u30D9\u30EB\u6570\
    )\n */\ntemplate< template< typename > class FPS, typename Mint >\nFPS< Mint >\
    \ bell(int N) {\n  FPS< Mint > poly(N + 1), ret(N + 1);\n  poly[1] = 1;\n  poly\
    \ = poly.exp();\n  poly[0] -= 1;\n  poly = poly.exp();\n  FPS mul = 1;\n  for(int\
    \ i = 0; i <= N; i++) {\n    ret[i] = poly[i] * mul;\n    mul *= i + 1;\n  }\n\
    \  return ret;\n}\n"
  code: "/**\n * @brief Bell(\u30D9\u30EB\u6570)\n */\ntemplate< template< typename\
    \ > class FPS, typename Mint >\nFPS< Mint > bell(int N) {\n  FPS< Mint > poly(N\
    \ + 1), ret(N + 1);\n  poly[1] = 1;\n  poly = poly.exp();\n  poly[0] -= 1;\n \
    \ poly = poly.exp();\n  FPS mul = 1;\n  for(int i = 0; i <= N; i++) {\n    ret[i]\
    \ = poly[i] * mul;\n    mul *= i + 1;\n  }\n  return ret;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fps/bell.cpp
  requiredBy: []
  timestamp: '2021-07-03 01:30:39+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: math/fps/bell.cpp
layout: document
redirect_from:
- /library/math/fps/bell.cpp
- /library/math/fps/bell.cpp.html
title: "Bell(\u30D9\u30EB\u6570)"
---
