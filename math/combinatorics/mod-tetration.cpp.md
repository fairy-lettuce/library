---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-tetration-mod.test.cpp
    title: test/verify/yosupo-tetration-mod.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    document_title: Mod-Tetration
    links: []
  bundledCode: "#line 1 \"math/combinatorics/mod-tetration.cpp\"\n/**\n * @brief Mod-Tetration\n\
    \ */\ntemplate< typename T >\nT mod_tetration(const T &a, const T &b, const T\
    \ &m) {\n  if(m == 1) return 0;\n  if(a == 0) return !(b & 1);\n  if(b == 0) return\
    \ 1;\n  if(b == 1) return a % m;\n  if(b == 2) return mod_pow(a % m, a, m);\n\
    \  auto phi = euler_phi(m);\n  return mod_pow(a % m, mod_tetration(a, b - 1, phi)\
    \ + phi, m);\n}\n"
  code: "/**\n * @brief Mod-Tetration\n */\ntemplate< typename T >\nT mod_tetration(const\
    \ T &a, const T &b, const T &m) {\n  if(m == 1) return 0;\n  if(a == 0) return\
    \ !(b & 1);\n  if(b == 0) return 1;\n  if(b == 1) return a % m;\n  if(b == 2)\
    \ return mod_pow(a % m, a, m);\n  auto phi = euler_phi(m);\n  return mod_pow(a\
    \ % m, mod_tetration(a, b - 1, phi) + phi, m);\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/combinatorics/mod-tetration.cpp
  requiredBy: []
  timestamp: '2020-03-03 18:28:13+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-tetration-mod.test.cpp
documentation_of: math/combinatorics/mod-tetration.cpp
layout: document
redirect_from:
- /library/math/combinatorics/mod-tetration.cpp
- /library/math/combinatorics/mod-tetration.cpp.html
title: Mod-Tetration
---
