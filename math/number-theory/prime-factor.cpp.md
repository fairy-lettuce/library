---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-ntl-1-a.test.cpp
    title: test/verify/aoj-ntl-1-a.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links: []
  bundledCode: "#line 1 \"math/number-theory/prime-factor.cpp\"\nmap< int64_t, int\
    \ > prime_factor(int64_t n) {\n  map< int64_t, int > ret;\n  for(int64_t i = 2;\
    \ i * i <= n; i++) {\n    while(n % i == 0) {\n      ret[i]++;\n      n /= i;\n\
    \    }\n  }\n  if(n != 1) ret[n] = 1;\n  return ret;\n}\n"
  code: "map< int64_t, int > prime_factor(int64_t n) {\n  map< int64_t, int > ret;\n\
    \  for(int64_t i = 2; i * i <= n; i++) {\n    while(n % i == 0) {\n      ret[i]++;\n\
    \      n /= i;\n    }\n  }\n  if(n != 1) ret[n] = 1;\n  return ret;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/number-theory/prime-factor.cpp
  requiredBy: []
  timestamp: '2019-11-30 23:36:31+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-ntl-1-a.test.cpp
documentation_of: math/number-theory/prime-factor.cpp
layout: document
redirect_from:
- /library/math/number-theory/prime-factor.cpp
- /library/math/number-theory/prime-factor.cpp.html
title: math/number-theory/prime-factor.cpp
---
