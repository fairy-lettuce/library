---
data:
  _extendedDependsOn: []
  _extendedRequiredBy:
  - icon: ':warning:'
    path: math/fps/factorial.cpp
    title: "Factorial(\u968E\u4E57)"
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    document_title: Sample-Point-Shift
    links: []
  bundledCode: "#line 1 \"math/fps/sample-point-shift.cpp\"\n/**\n * @brief Sample-Point-Shift\n\
    \ */\ntemplate< template< typename > class FPS, typename Mint >\nFPS< Mint > sample_point_shift(const\
    \ FPS< Mint > &ys, const Mint &m) {\n  Enumeration< Mint > comb;\n  int d = (int)\
    \ ys.size() - 1;\n  FPS< Mint > f(d + 1), g(d * 2 + 1);\n  for(int i = 0; i <=\
    \ d; i++) {\n    f[i] = ys[i] * comb.finv(i) * comb.finv(d - i);\n    if((d -\
    \ i) & 1) f[i] = -f[i];\n  }\n  for(int i = 0; i <= 2 * d; i++) {\n    g[i] =\
    \ modint(1) / (m - d + i);\n  }\n  auto h = f * g;\n  Mint coef = 1;\n  for(int\
    \ i = 0; i <= d; i++) {\n    coef *= (m - d + i);\n  }\n  for(int i = 0; i <=\
    \ d; i++) {\n    h[i + d] *= coef;\n    coef *= (m + i + 1) * g[i];\n  }\n  return\
    \ FPS< Mint >{begin(h) + d, begin(h) + 2 * d + 1};\n}\n"
  code: "/**\n * @brief Sample-Point-Shift\n */\ntemplate< template< typename > class\
    \ FPS, typename Mint >\nFPS< Mint > sample_point_shift(const FPS< Mint > &ys,\
    \ const Mint &m) {\n  Enumeration< Mint > comb;\n  int d = (int) ys.size() - 1;\n\
    \  FPS< Mint > f(d + 1), g(d * 2 + 1);\n  for(int i = 0; i <= d; i++) {\n    f[i]\
    \ = ys[i] * comb.finv(i) * comb.finv(d - i);\n    if((d - i) & 1) f[i] = -f[i];\n\
    \  }\n  for(int i = 0; i <= 2 * d; i++) {\n    g[i] = modint(1) / (m - d + i);\n\
    \  }\n  auto h = f * g;\n  Mint coef = 1;\n  for(int i = 0; i <= d; i++) {\n \
    \   coef *= (m - d + i);\n  }\n  for(int i = 0; i <= d; i++) {\n    h[i + d] *=\
    \ coef;\n    coef *= (m + i + 1) * g[i];\n  }\n  return FPS< Mint >{begin(h) +\
    \ d, begin(h) + 2 * d + 1};\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fps/sample-point-shift.cpp
  requiredBy:
  - math/fps/factorial.cpp
  timestamp: '2021-06-29 01:28:49+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: math/fps/sample-point-shift.cpp
layout: document
redirect_from:
- /library/math/fps/sample-point-shift.cpp
- /library/math/fps/sample-point-shift.cpp.html
title: Sample-Point-Shift
---
