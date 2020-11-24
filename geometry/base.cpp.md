---
data:
  _extendedDependsOn: []
  _extendedRequiredBy:
  - icon: ':warning:'
    path: geometry/angle.cpp
    title: geometry/angle.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/ccw.cpp
    title: geometry/ccw.cpp
  - icon: ':warning:'
    path: geometry/circle.cpp
    title: geometry/circle.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/is_orthogonal.cpp
    title: geometry/is_orthogonal.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/is_parallel.cpp
    title: geometry/is_parallel.cpp
  - icon: ':question:'
    path: geometry/line.cpp
    title: geometry/line.cpp
  - icon: ':question:'
    path: geometry/point.cpp
    title: geometry/point.cpp
  - icon: ':x:'
    path: geometry/projection.cpp
    title: geometry/projection.cpp
  - icon: ':warning:'
    path: geometry/reflection.cpp
    title: geometry/reflection.cpp
  - icon: ':warning:'
    path: geometry/segment.cpp
    title: geometry/segment.cpp
  _extendedVerifiedWith:
  - icon: ':x:'
    path: test/verify/aoj-cgl-1-a.test.cpp
    title: test/verify/aoj-cgl-1-a.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-cgl-1-c.test.cpp
    title: test/verify/aoj-cgl-1-c.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-cgl-2-a.test.cpp
    title: test/verify/aoj-cgl-2-a.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':question:'
  attributes:
    links: []
  bundledCode: "#line 2 \"geometry/base.cpp\"\n\nnamespace geometry {\n  using Real\
    \ = double;\n  const Real EPS = 1e-8;\n  const Real PI = acos(static_cast< Real\
    \ >(-1));\n\n  inline int sign(const Real &r) {\n    return r <= -EPS ? -1 : r\
    \ >= EPS ? 1 : 0;\n  }\n\n  inline bool equals(const Real &a, const Real &b) {\n\
    \    return sign(a - b) == 0;\n  }\n}\n"
  code: "#pragma once\n\nnamespace geometry {\n  using Real = double;\n  const Real\
    \ EPS = 1e-8;\n  const Real PI = acos(static_cast< Real >(-1));\n\n  inline int\
    \ sign(const Real &r) {\n    return r <= -EPS ? -1 : r >= EPS ? 1 : 0;\n  }\n\n\
    \  inline bool equals(const Real &a, const Real &b) {\n    return sign(a - b)\
    \ == 0;\n  }\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: geometry/base.cpp
  requiredBy:
  - geometry/reflection.cpp
  - geometry/line.cpp
  - geometry/circle.cpp
  - geometry/is_orthogonal.cpp
  - geometry/angle.cpp
  - geometry/projection.cpp
  - geometry/ccw.cpp
  - geometry/is_parallel.cpp
  - geometry/segment.cpp
  - geometry/point.cpp
  timestamp: '2020-11-24 18:23:37+09:00'
  verificationStatus: LIBRARY_SOME_WA
  verifiedWith:
  - test/verify/aoj-cgl-2-a.test.cpp
  - test/verify/aoj-cgl-1-c.test.cpp
  - test/verify/aoj-cgl-1-a.test.cpp
documentation_of: geometry/base.cpp
layout: document
redirect_from:
- /library/geometry/base.cpp
- /library/geometry/base.cpp.html
title: geometry/base.cpp
---
