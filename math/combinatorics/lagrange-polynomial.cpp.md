---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 1 \"math/combinatorics/lagrange-polynomial.cpp\"\ntemplate<\
    \ typename T >\nT lagrange_polynomial(const vector< T > &y, int64_t t) {\n  int\
    \ N = y.size() - 1;\n  Combination< T > comb(N);\n  if(t <= N) return y[t];\n\
    \  T ret(0);\n  vector< T > dp(N + 1, 1), pd(N + 1, 1);\n  for(int i = 0; i <\
    \ N; i++) dp[i + 1] = dp[i] * (t - i);\n  for(int i = N; i > 0; i--) pd[i - 1]\
    \ = pd[i] * (t - i);\n  for(int i = 0; i <= N; i++) {\n    T tmp = y[i] * dp[i]\
    \ * pd[i] * comb.rfact(i) * comb.rfact(N - i);\n    if((N - i) & 1) ret -= tmp;\n\
    \    else ret += tmp;\n  }\n  return ret;\n}\n"
  code: "template< typename T >\nT lagrange_polynomial(const vector< T > &y, int64_t\
    \ t) {\n  int N = y.size() - 1;\n  Combination< T > comb(N);\n  if(t <= N) return\
    \ y[t];\n  T ret(0);\n  vector< T > dp(N + 1, 1), pd(N + 1, 1);\n  for(int i =\
    \ 0; i < N; i++) dp[i + 1] = dp[i] * (t - i);\n  for(int i = N; i > 0; i--) pd[i\
    \ - 1] = pd[i] * (t - i);\n  for(int i = 0; i <= N; i++) {\n    T tmp = y[i] *\
    \ dp[i] * pd[i] * comb.rfact(i) * comb.rfact(N - i);\n    if((N - i) & 1) ret\
    \ -= tmp;\n    else ret += tmp;\n  }\n  return ret;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/combinatorics/lagrange-polynomial.cpp
  requiredBy: []
  timestamp: '2019-11-30 23:36:31+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: math/combinatorics/lagrange-polynomial.cpp
layout: document
redirect_from:
- /library/math/combinatorics/lagrange-polynomial.cpp
- /library/math/combinatorics/lagrange-polynomial.cpp.html
title: math/combinatorics/lagrange-polynomial.cpp
---
