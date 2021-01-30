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
  bundledCode: "#line 1 \"math/number-theory/moebius-mu-table.cpp\"\nvector< int >\
    \ moebius_mu_table(int n) {\n  vector< int > mu(n + 1, 1), p(n + 1, 1);\n  for(int\
    \ i = 2; i <= n; i++) {\n    if(p[i] == 1) {\n      for(int j = i; j <= n; j +=\
    \ i) p[j] = i;\n    }\n    if((i / p[i]) % p[i] == 0) mu[i] = 0;\n    else mu[i]\
    \ = -mu[i / p[i]];\n  }\n  return mu;\n}\n"
  code: "vector< int > moebius_mu_table(int n) {\n  vector< int > mu(n + 1, 1), p(n\
    \ + 1, 1);\n  for(int i = 2; i <= n; i++) {\n    if(p[i] == 1) {\n      for(int\
    \ j = i; j <= n; j += i) p[j] = i;\n    }\n    if((i / p[i]) % p[i] == 0) mu[i]\
    \ = 0;\n    else mu[i] = -mu[i / p[i]];\n  }\n  return mu;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/number-theory/moebius-mu-table.cpp
  requiredBy: []
  timestamp: '2020-01-16 16:18:06+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: math/number-theory/moebius-mu-table.cpp
layout: document
redirect_from:
- /library/math/number-theory/moebius-mu-table.cpp
- /library/math/number-theory/moebius-mu-table.cpp.html
title: math/number-theory/moebius-mu-table.cpp
---
