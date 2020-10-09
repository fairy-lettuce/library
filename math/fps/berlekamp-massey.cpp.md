---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-find-linear-recurrence.test.cpp
    title: test/verify/yosupo-find-linear-recurrence.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-sparse-matrix-det.test.cpp
    title: test/verify/yosupo-sparse-matrix-det.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links: []
  bundledCode: "#line 1 \"math/fps/berlekamp-massey.cpp\"\ntemplate< class T >\nFormalPowerSeries<\
    \ T > berlekamp_massey(const FormalPowerSeries< T > &s) {\n  const int N = (int)\
    \ s.size();\n  FormalPowerSeries< T > b = {T(-1)}, c = {T(-1)};\n  T y = T(1);\n\
    \  for(int ed = 1; ed <= N; ed++) {\n    int l = int(c.size()), m = int(b.size());\n\
    \    T x = 0;\n    for(int i = 0; i < l; i++) x += c[i] * s[ed - l + i];\n   \
    \ b.emplace_back(0);\n    m++;\n    if(x == T(0)) continue;\n    T freq = x /\
    \ y;\n    if(l < m) {\n      auto tmp = c;\n      c.insert(begin(c), m - l, T(0));\n\
    \      for(int i = 0; i < m; i++) c[m - 1 - i] -= freq * b[m - 1 - i];\n     \
    \ b = tmp;\n      y = x;\n    } else {\n      for(int i = 0; i < m; i++) c[l -\
    \ 1 - i] -= freq * b[m - 1 - i];\n    }\n  }\n  return c;\n}\n"
  code: "template< class T >\nFormalPowerSeries< T > berlekamp_massey(const FormalPowerSeries<\
    \ T > &s) {\n  const int N = (int) s.size();\n  FormalPowerSeries< T > b = {T(-1)},\
    \ c = {T(-1)};\n  T y = T(1);\n  for(int ed = 1; ed <= N; ed++) {\n    int l =\
    \ int(c.size()), m = int(b.size());\n    T x = 0;\n    for(int i = 0; i < l; i++)\
    \ x += c[i] * s[ed - l + i];\n    b.emplace_back(0);\n    m++;\n    if(x == T(0))\
    \ continue;\n    T freq = x / y;\n    if(l < m) {\n      auto tmp = c;\n     \
    \ c.insert(begin(c), m - l, T(0));\n      for(int i = 0; i < m; i++) c[m - 1 -\
    \ i] -= freq * b[m - 1 - i];\n      b = tmp;\n      y = x;\n    } else {\n   \
    \   for(int i = 0; i < m; i++) c[l - 1 - i] -= freq * b[m - 1 - i];\n    }\n \
    \ }\n  return c;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fps/berlekamp-massey.cpp
  requiredBy: []
  timestamp: '2019-11-30 23:36:31+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-find-linear-recurrence.test.cpp
  - test/verify/yosupo-sparse-matrix-det.test.cpp
documentation_of: math/fps/berlekamp-massey.cpp
layout: document
redirect_from:
- /library/math/fps/berlekamp-massey.cpp
- /library/math/fps/berlekamp-massey.cpp.html
title: math/fps/berlekamp-massey.cpp
---
