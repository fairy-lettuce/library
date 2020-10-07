---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-alds-1-1-c-2.test.cpp
    title: test/verify/aoj-alds-1-1-c-2.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-counting-primes.test.cpp
    title: test/verify/yosupo-counting-primes.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links: []
  bundledCode: "#line 1 \"math/number-theory/prime-table.cpp\"\nvector< bool > prime_table(int\
    \ n) {\n  vector< bool > prime(n + 1, true);\n  if(n >= 0) prime[0] = false;\n\
    \  if(n >= 1) prime[1] = false;\n  for(int i = 2; i * i <= n; i++) {\n    if(!prime[i])\
    \ continue;\n    for(int j = i + i; j <= n; j += i) {\n      prime[j] = false;\n\
    \    }\n  }\n  return prime;\n}\n"
  code: "vector< bool > prime_table(int n) {\n  vector< bool > prime(n + 1, true);\n\
    \  if(n >= 0) prime[0] = false;\n  if(n >= 1) prime[1] = false;\n  for(int i =\
    \ 2; i * i <= n; i++) {\n    if(!prime[i]) continue;\n    for(int j = i + i; j\
    \ <= n; j += i) {\n      prime[j] = false;\n    }\n  }\n  return prime;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/number-theory/prime-table.cpp
  requiredBy: []
  timestamp: '2019-11-30 23:36:31+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-counting-primes.test.cpp
  - test/verify/aoj-alds-1-1-c-2.test.cpp
documentation_of: math/number-theory/prime-table.cpp
layout: document
redirect_from:
- /library/math/number-theory/prime-table.cpp
- /library/math/number-theory/prime-table.cpp.html
title: math/number-theory/prime-table.cpp
---
