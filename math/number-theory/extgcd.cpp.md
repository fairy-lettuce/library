---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-ntl-1-e.test.cpp
    title: test/verify/aoj-ntl-1-e.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    links: []
  bundledCode: "#line 1 \"math/number-theory/extgcd.cpp\"\ntemplate< typename T >\n\
    T extgcd(T a, T b, T &x, T &y) {\n  T d = a;\n  if(b != 0) {\n    d = extgcd(b,\
    \ a % b, y, x);\n    y -= (a / b) * x;\n  } else {\n    x = 1;\n    y = 0;\n \
    \ }\n  return d;\n}\n"
  code: "template< typename T >\nT extgcd(T a, T b, T &x, T &y) {\n  T d = a;\n  if(b\
    \ != 0) {\n    d = extgcd(b, a % b, y, x);\n    y -= (a / b) * x;\n  } else {\n\
    \    x = 1;\n    y = 0;\n  }\n  return d;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/number-theory/extgcd.cpp
  requiredBy: []
  timestamp: '2019-11-30 23:36:31+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-ntl-1-e.test.cpp
documentation_of: math/number-theory/extgcd.cpp
layout: document
redirect_from:
- /library/math/number-theory/extgcd.cpp
- /library/math/number-theory/extgcd.cpp.html
title: math/number-theory/extgcd.cpp
---
