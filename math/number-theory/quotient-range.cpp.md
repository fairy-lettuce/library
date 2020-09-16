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
  bundledCode: "#line 1 \"math/number-theory/quotient-range.cpp\"\ntemplate< typename\
    \ T >\nvector< pair< pair< T, T >, T > > quotient_range(T N) {\n  T M;\n  vector<\
    \ pair< pair< T, T >, T > > ret;\n  for(M = 1; M * M <= N; M++) {\n    ret.emplace_back(make_pair(M,\
    \ M), N / M);\n  }\n  for(T i = M; i >= 1; i--) {\n    T L = N / (i + 1) + 1;\n\
    \    T R = N / i;\n    if(L <= R && ret.back().first.second < L) ret.emplace_back(make_pair(L,\
    \ R), N / L);\n  }\n  return ret;\n}\n"
  code: "template< typename T >\nvector< pair< pair< T, T >, T > > quotient_range(T\
    \ N) {\n  T M;\n  vector< pair< pair< T, T >, T > > ret;\n  for(M = 1; M * M <=\
    \ N; M++) {\n    ret.emplace_back(make_pair(M, M), N / M);\n  }\n  for(T i = M;\
    \ i >= 1; i--) {\n    T L = N / (i + 1) + 1;\n    T R = N / i;\n    if(L <= R\
    \ && ret.back().first.second < L) ret.emplace_back(make_pair(L, R), N / L);\n\
    \  }\n  return ret;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/number-theory/quotient-range.cpp
  requiredBy: []
  timestamp: '2019-11-30 23:36:31+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: math/number-theory/quotient-range.cpp
layout: document
redirect_from:
- /library/math/number-theory/quotient-range.cpp
- /library/math/number-theory/quotient-range.cpp.html
title: math/number-theory/quotient-range.cpp
---
