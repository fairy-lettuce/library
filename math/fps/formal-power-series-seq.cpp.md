---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-bellnoulli-number.test.cpp
    title: test/verify/yosupo-bellnoulli-number.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-partition-function.test.cpp
    title: test/verify/yosupo-partition-function.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links: []
  bundledCode: "#line 1 \"math/fps/formal-power-series-seq.cpp\"\ntemplate< typename\
    \ T >\nFormalPowerSeries< T > bernoulli(int N) {\n  FormalPowerSeries< T > poly(N\
    \ + 1);\n  poly[0] = T(1);\n  for(int i = 1; i <= N; i++) {\n    poly[i] = poly[i\
    \ - 1] / T(i + 1);\n  }\n  poly = poly.inv();\n  T tmp(1);\n  for(int i = 1; i\
    \ <= N; i++) {\n    tmp *= T(i);\n    poly[i] *= tmp;\n  }\n  return poly;\n}\n\
    \ntemplate< typename T >\nFormalPowerSeries< T > partition(int N) {\n  FormalPowerSeries<\
    \ T > poly(N + 1);\n  poly[0] = 1;\n  for(int k = 1; k <= N; k++) {\n    if(1LL\
    \ * k * (3 * k + 1) / 2 <= N) poly[k * (3 * k + 1) / 2] += (k % 2 ? -1 : 1);\n\
    \    if(1LL * k * (3 * k - 1) / 2 <= N) poly[k * (3 * k - 1) / 2] += (k % 2 ?\
    \ -1 : 1);\n  }\n  return poly.inv();\n}\n\ntemplate< typename T >\nFormalPowerSeries<\
    \ T > bell(int N) {\n  FormalPowerSeries< T > poly(N + 1), ret(N + 1);\n  poly[1]\
    \ = 1;\n  poly = poly.exp();\n  poly[0] -= 1;\n  poly = poly.exp();\n  T mul =\
    \ 1;\n  for(int i = 0; i <= N; i++) {\n    ret[i] = poly[i] * mul;\n    mul *=\
    \ i + 1;\n  }\n  return ret;\n}\n\ntemplate< typename T >\nFormalPowerSeries<\
    \ T > stirling_first(int N) {\n  if(N == 0) return {1};\n  int M = N / 2;\n  FormalPowerSeries<\
    \ T > A = stirling_first< T >(M), B, C(N - M + 1);\n\n  if(N % 2 == 0) {\n   \
    \ B = A;\n  } else {\n    B.resize(M + 2);\n    B[M + 1] = 1;\n    for(int i =\
    \ 1; i < M + 1; i++) B[i] = A[i - 1] + A[i] * M;\n  }\n\n  T tmp = 1;\n  for(int\
    \ i = 0; i <= N - M; i++) {\n    C[N - M - i] = T(M).pow(i) / tmp;\n    B[i] *=\
    \ tmp;\n    tmp *= T(i + 1);\n  }\n  C *= B;\n  tmp = 1;\n  for(int i = 0; i <=\
    \ N - M; i++) {\n    B[i] = C[N - M + i] / tmp;\n    tmp *= T(i + 1);\n  }\n \
    \ return A * B;\n}\n\ntemplate< typename T >\nFormalPowerSeries< T > stirling_second(int\
    \ N) {\n  FormalPowerSeries< T > A(N + 1), B(N + 1);\n  modint tmp = 1;\n  for(int\
    \ i = 0; i <= N; i++) {\n    T rev = T(1) / tmp;\n    A[i] = T(i).pow(N) * rev;\n\
    \    B[i] = T(1) * rev;\n    if(i & 1) B[i] *= -1;\n    tmp *= i + 1;\n  }\n \
    \ return (A * B).pre(N + 1);\n}\n\ntemplate< typename T >\nFormalPowerSeries<\
    \ T > stirling_second_kth_column(int N, int K) {\n  FormalPowerSeries< T > poly(N\
    \ + 1), ret(N + 1);\n  poly[1] = 1;\n  poly = poly.exp();\n  poly[0] -= 1;\n \
    \ poly = poly.pow(K);\n  T rev = 1, mul = 1;\n  for(int i = 2; i <= K; i++) rev\
    \ *= i;\n  rev = T(1) / rev;\n  poly *= rev;\n  for(int i = 0; i <= N; i++) {\n\
    \    ret[i] = poly[i] * mul;\n    mul *= i + 1;\n  }\n  return ret;\n}\n\ntemplate<\
    \ typename T >\nFormalPowerSeries< T > eulerian(int N) {\n  vector< T > fact(N\
    \ + 2), rfact(N + 2);\n  fact[0] = rfact[N + 1] = 1;\n  for(int i = 1; i <= N\
    \ + 1; i++) fact[i] = fact[i - 1] * i;\n  rfact[N + 1] /= fact[N + 1];\n  for(int\
    \ i = N; i >= 0; i--) rfact[i] = rfact[i + 1] * (i + 1);\n\n  FormalPowerSeries<\
    \ T > A(N + 1), B(N + 1);\n  for(int i = 0; i <= N; i++) {\n    A[i] = fact[N\
    \ + 1] * rfact[i] * rfact[N + 1 - i];\n    if(i & 1) A[i] *= -1;\n    B[i] = T(i\
    \ + 1).pow(N);\n  }\n  return (A * B).pre(N + 1);\n}\n"
  code: "template< typename T >\nFormalPowerSeries< T > bernoulli(int N) {\n  FormalPowerSeries<\
    \ T > poly(N + 1);\n  poly[0] = T(1);\n  for(int i = 1; i <= N; i++) {\n    poly[i]\
    \ = poly[i - 1] / T(i + 1);\n  }\n  poly = poly.inv();\n  T tmp(1);\n  for(int\
    \ i = 1; i <= N; i++) {\n    tmp *= T(i);\n    poly[i] *= tmp;\n  }\n  return\
    \ poly;\n}\n\ntemplate< typename T >\nFormalPowerSeries< T > partition(int N)\
    \ {\n  FormalPowerSeries< T > poly(N + 1);\n  poly[0] = 1;\n  for(int k = 1; k\
    \ <= N; k++) {\n    if(1LL * k * (3 * k + 1) / 2 <= N) poly[k * (3 * k + 1) /\
    \ 2] += (k % 2 ? -1 : 1);\n    if(1LL * k * (3 * k - 1) / 2 <= N) poly[k * (3\
    \ * k - 1) / 2] += (k % 2 ? -1 : 1);\n  }\n  return poly.inv();\n}\n\ntemplate<\
    \ typename T >\nFormalPowerSeries< T > bell(int N) {\n  FormalPowerSeries< T >\
    \ poly(N + 1), ret(N + 1);\n  poly[1] = 1;\n  poly = poly.exp();\n  poly[0] -=\
    \ 1;\n  poly = poly.exp();\n  T mul = 1;\n  for(int i = 0; i <= N; i++) {\n  \
    \  ret[i] = poly[i] * mul;\n    mul *= i + 1;\n  }\n  return ret;\n}\n\ntemplate<\
    \ typename T >\nFormalPowerSeries< T > stirling_first(int N) {\n  if(N == 0) return\
    \ {1};\n  int M = N / 2;\n  FormalPowerSeries< T > A = stirling_first< T >(M),\
    \ B, C(N - M + 1);\n\n  if(N % 2 == 0) {\n    B = A;\n  } else {\n    B.resize(M\
    \ + 2);\n    B[M + 1] = 1;\n    for(int i = 1; i < M + 1; i++) B[i] = A[i - 1]\
    \ + A[i] * M;\n  }\n\n  T tmp = 1;\n  for(int i = 0; i <= N - M; i++) {\n    C[N\
    \ - M - i] = T(M).pow(i) / tmp;\n    B[i] *= tmp;\n    tmp *= T(i + 1);\n  }\n\
    \  C *= B;\n  tmp = 1;\n  for(int i = 0; i <= N - M; i++) {\n    B[i] = C[N -\
    \ M + i] / tmp;\n    tmp *= T(i + 1);\n  }\n  return A * B;\n}\n\ntemplate< typename\
    \ T >\nFormalPowerSeries< T > stirling_second(int N) {\n  FormalPowerSeries< T\
    \ > A(N + 1), B(N + 1);\n  modint tmp = 1;\n  for(int i = 0; i <= N; i++) {\n\
    \    T rev = T(1) / tmp;\n    A[i] = T(i).pow(N) * rev;\n    B[i] = T(1) * rev;\n\
    \    if(i & 1) B[i] *= -1;\n    tmp *= i + 1;\n  }\n  return (A * B).pre(N + 1);\n\
    }\n\ntemplate< typename T >\nFormalPowerSeries< T > stirling_second_kth_column(int\
    \ N, int K) {\n  FormalPowerSeries< T > poly(N + 1), ret(N + 1);\n  poly[1] =\
    \ 1;\n  poly = poly.exp();\n  poly[0] -= 1;\n  poly = poly.pow(K);\n  T rev =\
    \ 1, mul = 1;\n  for(int i = 2; i <= K; i++) rev *= i;\n  rev = T(1) / rev;\n\
    \  poly *= rev;\n  for(int i = 0; i <= N; i++) {\n    ret[i] = poly[i] * mul;\n\
    \    mul *= i + 1;\n  }\n  return ret;\n}\n\ntemplate< typename T >\nFormalPowerSeries<\
    \ T > eulerian(int N) {\n  vector< T > fact(N + 2), rfact(N + 2);\n  fact[0] =\
    \ rfact[N + 1] = 1;\n  for(int i = 1; i <= N + 1; i++) fact[i] = fact[i - 1] *\
    \ i;\n  rfact[N + 1] /= fact[N + 1];\n  for(int i = N; i >= 0; i--) rfact[i] =\
    \ rfact[i + 1] * (i + 1);\n\n  FormalPowerSeries< T > A(N + 1), B(N + 1);\n  for(int\
    \ i = 0; i <= N; i++) {\n    A[i] = fact[N + 1] * rfact[i] * rfact[N + 1 - i];\n\
    \    if(i & 1) A[i] *= -1;\n    B[i] = T(i + 1).pow(N);\n  }\n  return (A * B).pre(N\
    \ + 1);\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fps/formal-power-series-seq.cpp
  requiredBy: []
  timestamp: '2019-11-30 23:36:31+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-partition-function.test.cpp
  - test/verify/yosupo-bellnoulli-number.test.cpp
documentation_of: math/fps/formal-power-series-seq.cpp
layout: document
redirect_from:
- /library/math/fps/formal-power-series-seq.cpp
- /library/math/fps/formal-power-series-seq.cpp.html
title: math/fps/formal-power-series-seq.cpp
---
