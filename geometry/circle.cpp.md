---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: geometry/base.cpp
    title: geometry/base.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/point.cpp
    title: geometry/point.cpp
  _extendedRequiredBy:
  - icon: ':heavy_check_mark:'
    path: geometry/cross_point_cc.cpp
    title: geometry/cross_point_cc.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/cross_point_cl.cpp
    title: geometry/cross_point_cl.cpp
  - icon: ':warning:'
    path: geometry/cross_point_cs.cpp
    title: geometry/cross_point_cs.cpp
  - icon: ':warning:'
    path: geometry/is_intersect_cl.cpp
    title: geometry/is_intersect_cl.cpp
  - icon: ':warning:'
    path: geometry/is_intersect_cp.cpp
    title: geometry/is_intersect_cp.cpp
  - icon: ':warning:'
    path: geometry/is_intersect_cs.cpp
    title: geometry/is_intersect_cs.cpp
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-cgl-7-d.test.cpp
    title: test/verify/aoj-cgl-7-d.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-cgl-7-e.test.cpp
    title: test/verify/aoj-cgl-7-e.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links: []
  bundledCode: "#line 2 \"geometry/base.cpp\"\n\nnamespace geometry {\n  using Real\
    \ = double;\n  const Real EPS = 1e-8;\n  const Real PI = acos(static_cast< Real\
    \ >(-1));\n\n  enum {\n    OUT, ON, IN\n  };\n\n  inline int sign(const Real &r)\
    \ {\n    return r <= -EPS ? -1 : r >= EPS ? 1 : 0;\n  }\n\n  inline bool equals(const\
    \ Real &a, const Real &b) {\n    return sign(a - b) == 0;\n  }\n}\n#line 3 \"\
    geometry/point.cpp\"\n\nnamespace geometry {\n  using Point = complex< Real >;\n\
    \n  istream &operator>>(istream &is, Point &p) {\n    Real a, b;\n    is >> a\
    \ >> b;\n    p = Point(a, b);\n    return is;\n  }\n\n  ostream &operator<<(ostream\
    \ &os, const Point &p) {\n    return os << real(p) << \" \" << imag(p);\n  }\n\
    \n  Point operator*(const Point &p, const Real &d) {\n    return Point(real(p)\
    \ * d, imag(p) * d);\n  }\n\n  // rotate point p counterclockwise by theta rad\n\
    \  Point rotate(Real theta, const Point &p) {\n    return Point(cos(theta) * real(p)\
    \ - sin(theta) * imag(p), sin(theta) * real(p) + cos(theta) * imag(p));\n  }\n\
    \n  Real cross(const Point &a, const Point &b) {\n    return real(a) * imag(b)\
    \ - imag(a) * real(b);\n  }\n\n  Real dot(const Point &a, const Point &b) {\n\
    \    return real(a) * real(b) + imag(a) * imag(b);\n  }\n\n  bool compare_x(const\
    \ Point &a, const Point &b) {\n    return equals(real(a), real(b)) ? imag(a) <\
    \ imag(b) : real(a) < real(b);\n  }\n\n  bool compare_y(const Point &a, const\
    \ Point &b) {\n    return equals(imag(a), imag(b)) ? real(a) < real(b) : imag(a)\
    \ < imag(b);\n  }\n\n  using Points = vector< Point >;\n}\n#line 3 \"geometry/circle.cpp\"\
    \n\nnamespace geometry {\n  struct Circle {\n    Point p;\n    Real r{};\n\n \
    \   Circle() = default;\n\n    Circle(const Point &p, const Real &r) : p(p), r(r)\
    \ {}\n  };\n\n  using Circles = vector< Circle >;\n}\n"
  code: "#pragma once\n#include \"point.cpp\"\n\nnamespace geometry {\n  struct Circle\
    \ {\n    Point p;\n    Real r{};\n\n    Circle() = default;\n\n    Circle(const\
    \ Point &p, const Real &r) : p(p), r(r) {}\n  };\n\n  using Circles = vector<\
    \ Circle >;\n}\n"
  dependsOn:
  - geometry/point.cpp
  - geometry/base.cpp
  isVerificationFile: false
  path: geometry/circle.cpp
  requiredBy:
  - geometry/cross_point_cl.cpp
  - geometry/is_intersect_cs.cpp
  - geometry/is_intersect_cl.cpp
  - geometry/cross_point_cs.cpp
  - geometry/cross_point_cc.cpp
  - geometry/is_intersect_cp.cpp
  timestamp: '2020-12-01 17:38:42+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-cgl-7-e.test.cpp
  - test/verify/aoj-cgl-7-d.test.cpp
documentation_of: geometry/circle.cpp
layout: document
redirect_from:
- /library/geometry/circle.cpp
- /library/geometry/circle.cpp.html
title: geometry/circle.cpp
---
