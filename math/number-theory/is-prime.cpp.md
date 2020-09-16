---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-alds-1-1-c.test.cpp
    title: test/verify/aoj-alds-1-1-c.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    links: []
  bundledCode: "#line 1 \"math/number-theory/is-prime.cpp\"\nbool is_prime(int64_t\
    \ x) {\n  for(int64_t i = 2; i * i <= x; i++) {\n    if(x % i == 0) return false;\n\
    \  }\n  return true;\n}\n"
  code: "bool is_prime(int64_t x) {\n  for(int64_t i = 2; i * i <= x; i++) {\n   \
    \ if(x % i == 0) return false;\n  }\n  return true;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/number-theory/is-prime.cpp
  requiredBy: []
  timestamp: '2019-11-30 23:36:31+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-alds-1-1-c.test.cpp
documentation_of: math/number-theory/is-prime.cpp
layout: document
redirect_from:
- /library/math/number-theory/is-prime.cpp
- /library/math/number-theory/is-prime.cpp.html
title: math/number-theory/is-prime.cpp
---
