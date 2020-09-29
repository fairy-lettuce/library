---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-dpl-5-i.test.cpp
    title: test/verify/aoj-dpl-5-i.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links: []
  bundledCode: "#line 1 \"math/combinatorics/stirling-number-second.cpp\"\ntemplate<\
    \ typename T >\nT stirling_number_second(int n, int k) {\n  Combination< T > table(k);\n\
    \  T ret = 0;\n  for(int i = 0; i <= k; i++) {\n    auto add = T(i).pow(n) * table.C(k,\
    \ i);\n    if((k - i) & 1) ret -= add;\n    else ret += add;\n  }\n  return ret\
    \ * table.rfact(k);\n}\n\n"
  code: "template< typename T >\nT stirling_number_second(int n, int k) {\n  Combination<\
    \ T > table(k);\n  T ret = 0;\n  for(int i = 0; i <= k; i++) {\n    auto add =\
    \ T(i).pow(n) * table.C(k, i);\n    if((k - i) & 1) ret -= add;\n    else ret\
    \ += add;\n  }\n  return ret * table.rfact(k);\n}\n\n"
  dependsOn: []
  isVerificationFile: false
  path: math/combinatorics/stirling-number-second.cpp
  requiredBy: []
  timestamp: '2019-11-30 23:36:31+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-dpl-5-i.test.cpp
documentation_of: math/combinatorics/stirling-number-second.cpp
layout: document
redirect_from:
- /library/math/combinatorics/stirling-number-second.cpp
- /library/math/combinatorics/stirling-number-second.cpp.html
title: math/combinatorics/stirling-number-second.cpp
---
