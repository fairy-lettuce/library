---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: geometry/base.cpp
    title: geometry/base.cpp
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
  - icon: ':heavy_check_mark:'
    path: geometry/line.cpp
    title: geometry/line.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/projection.cpp
    title: geometry/projection.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/reflection.cpp
    title: geometry/reflection.cpp
  - icon: ':warning:'
    path: geometry/segment.cpp
    title: geometry/segment.cpp
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-cgl-1-a.test.cpp
    title: test/verify/aoj-cgl-1-a.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-cgl-1-b.test.cpp
    title: test/verify/aoj-cgl-1-b.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-cgl-1-c.test.cpp
    title: test/verify/aoj-cgl-1-c.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-cgl-2-a.test.cpp
    title: test/verify/aoj-cgl-2-a.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links: []
  bundledCode: "#line 2 \"geometry/base.cpp\"\n\nnamespace geometry {\n  using Real\
    \ = double;\n  const Real EPS = 1e-8;\n  const Real PI = acos(static_cast< Real\
    \ >(-1));\n\n  inline int sign(const Real &r) {\n    return r <= -EPS ? -1 : r\
    \ >= EPS ? 1 : 0;\n  }\n\n  inline bool equals(const Real &a, const Real &b) {\n\
    \    return sign(a - b) == 0;\n  }\n}\n#line 3 \"geometry/point.cpp\"\n\nnamespace\
    \ geometry {\n  using Point = complex< Real >;\n\n  istream &operator>>(istream\
    \ &is, Point &p) {\n    Real a, b;\n    is >> a >> b;\n    p = Point(a, b);\n\
    \    return is;\n  }\n\n  ostream &operator<<(ostream &os, const Point &p) {\n\
    \    return os << real(p) << \" \" << imag(p);\n  }\n\n  Point operator*(const\
    \ Point &p, const Real &d) {\n    return Point(real(p) * d, imag(p) * d);\n  }\n\
    \n  // rotate point p counterclockwise by theta rad\n  Point rotate(Real theta,\
    \ const Point &p) {\n    return Point(cos(theta) * real(p) - sin(theta) * imag(p),\
    \ sin(theta) * real(p) + cos(theta) * imag(p));\n  }\n\n  Real cross(const Point\
    \ &a, const Point &b) {\n    return real(a) * imag(b) - imag(a) * real(b);\n \
    \ }\n\n  Real dot(const Point &a, const Point &b) {\n    return real(a) * real(b)\
    \ + imag(a) * imag(b);\n  }\n\n  using Points = vector< Point >;\n}\n"
  code: "#pragma once\n#include \"base.cpp\"\n\nnamespace geometry {\n  using Point\
    \ = complex< Real >;\n\n  istream &operator>>(istream &is, Point &p) {\n    Real\
    \ a, b;\n    is >> a >> b;\n    p = Point(a, b);\n    return is;\n  }\n\n  ostream\
    \ &operator<<(ostream &os, const Point &p) {\n    return os << real(p) << \" \"\
    \ << imag(p);\n  }\n\n  Point operator*(const Point &p, const Real &d) {\n   \
    \ return Point(real(p) * d, imag(p) * d);\n  }\n\n  // rotate point p counterclockwise\
    \ by theta rad\n  Point rotate(Real theta, const Point &p) {\n    return Point(cos(theta)\
    \ * real(p) - sin(theta) * imag(p), sin(theta) * real(p) + cos(theta) * imag(p));\n\
    \  }\n\n  Real cross(const Point &a, const Point &b) {\n    return real(a) * imag(b)\
    \ - imag(a) * real(b);\n  }\n\n  Real dot(const Point &a, const Point &b) {\n\
    \    return real(a) * real(b) + imag(a) * imag(b);\n  }\n\n  using Points = vector<\
    \ Point >;\n}\n"
  dependsOn:
  - geometry/base.cpp
  isVerificationFile: false
  path: geometry/point.cpp
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
  timestamp: '2020-11-24 18:23:37+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-cgl-2-a.test.cpp
  - test/verify/aoj-cgl-1-c.test.cpp
  - test/verify/aoj-cgl-1-a.test.cpp
  - test/verify/aoj-cgl-1-b.test.cpp
documentation_of: geometry/point.cpp
layout: document
redirect_from:
- /library/geometry/point.cpp
- /library/geometry/point.cpp.html
title: geometry/point.cpp
---
