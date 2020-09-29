---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-ntl-1-b.test.cpp
    title: test/verify/aoj-ntl-1-b.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-sqrt-mod.test.cpp
    title: test/verify/yosupo-sqrt-mod.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-sqrt-of-formal-power-series.test.cpp
    title: test/verify/yosupo-sqrt-of-formal-power-series.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-tetration-mod.test.cpp
    title: test/verify/yosupo-tetration-mod.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links: []
  bundledCode: "#line 1 \"math/combinatorics/mod-pow.cpp\"\ntemplate< typename T >\n\
    T mod_pow(T x, T n, const T &p) {\n  T ret = 1;\n  while(n > 0) {\n    if(n &\
    \ 1) (ret *= x) %= p;\n    (x *= x) %= p;\n    n >>= 1;\n  }\n  return ret;\n\
    }\n\n"
  code: "template< typename T >\nT mod_pow(T x, T n, const T &p) {\n  T ret = 1;\n\
    \  while(n > 0) {\n    if(n & 1) (ret *= x) %= p;\n    (x *= x) %= p;\n    n >>=\
    \ 1;\n  }\n  return ret;\n}\n\n"
  dependsOn: []
  isVerificationFile: false
  path: math/combinatorics/mod-pow.cpp
  requiredBy: []
  timestamp: '2019-11-30 23:36:31+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-sqrt-of-formal-power-series.test.cpp
  - test/verify/yosupo-tetration-mod.test.cpp
  - test/verify/aoj-ntl-1-b.test.cpp
  - test/verify/yosupo-sqrt-mod.test.cpp
documentation_of: math/combinatorics/mod-pow.cpp
layout: document
redirect_from:
- /library/math/combinatorics/mod-pow.cpp
- /library/math/combinatorics/mod-pow.cpp.html
title: math/combinatorics/mod-pow.cpp
---
