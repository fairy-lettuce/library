---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    links: []
  bundledCode: "#line 1 \"math/combinatorics/binomial.cpp\"\ntemplate< typename T\
    \ >\nT binomial(int64_t N, int64_t K) {\n  if(K < 0 || N < K) return 0;\n  T ret\
    \ = 1;\n  for(T i = 1; i <= K; ++i) {\n    ret *= N--;\n    ret /= i;\n  }\n \
    \ return ret;\n}\n"
  code: "template< typename T >\nT binomial(int64_t N, int64_t K) {\n  if(K < 0 ||\
    \ N < K) return 0;\n  T ret = 1;\n  for(T i = 1; i <= K; ++i) {\n    ret *= N--;\n\
    \    ret /= i;\n  }\n  return ret;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/combinatorics/binomial.cpp
  requiredBy: []
  timestamp: '2019-11-30 23:36:31+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: math/combinatorics/binomial.cpp
layout: document
redirect_from:
- /library/math/combinatorics/binomial.cpp
- /library/math/combinatorics/binomial.cpp.html
title: math/combinatorics/binomial.cpp
---
