---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: geometry/base.cpp
    title: geometry/base.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/point.cpp
    title: geometry/point.cpp
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
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
    \ + imag(a) * imag(b);\n  }\n\n  using Points = vector< Point >;\n}\n#line 3 \"\
    geometry/circle.cpp\"\n\nnamespace geometry {\n  struct Circle {\n    Point p;\n\
    \    Real r{};\n\n    Circle() = default;\n\n    Circle(const Point &p, const\
    \ Real &r) : p(p), r(r) {}\n  };\n\n  using Circles = vector< Segment >;\n}\n"
  code: "#pragma once\n#include \"point.cpp\"\n\nnamespace geometry {\n  struct Circle\
    \ {\n    Point p;\n    Real r{};\n\n    Circle() = default;\n\n    Circle(const\
    \ Point &p, const Real &r) : p(p), r(r) {}\n  };\n\n  using Circles = vector<\
    \ Segment >;\n}\n"
  dependsOn:
  - geometry/point.cpp
  - geometry/base.cpp
  isVerificationFile: false
  path: geometry/circle.cpp
  requiredBy: []
  timestamp: '2020-11-24 18:23:37+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: geometry/circle.cpp
layout: document
redirect_from:
- /library/geometry/circle.cpp
- /library/geometry/circle.cpp.html
title: geometry/circle.cpp
---
