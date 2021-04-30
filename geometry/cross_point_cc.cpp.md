---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: geometry/base.cpp
    title: geometry/base.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/circle.cpp
    title: geometry/circle.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/point.cpp
    title: geometry/point.cpp
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-cgl-7-e.test.cpp
    title: test/verify/aoj-cgl-7-e.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links:
    - http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=CGL_7_E
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
    \ {}\n  };\n\n  using Circles = vector< Circle >;\n}\n#line 4 \"geometry/cross_point_cc.cpp\"\
    \n\nnamespace geometry {\n  // http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=CGL_7_E\n\
    \  Points cross_point_cc(const Circle &c1, const Circle &c2) {\n    Real d = abs(c1.p\
    \ - c2.p), r = c1.r + c2.r;\n    if(sign(d - r) > 0 or sign(d + c1.r - c2.r) <\
    \ 0) return {};\n    Real a = acos((norm(c1.r) - norm(c2.r) + norm(d)) / (2 *\
    \ c1.r * d));\n    Real t = arg(c2.p - c1.p);\n    Point p = c1.p + polar(c1.r,\
    \ t + a);\n    Point q = c1.p + polar(c1.r, t - a);\n    if(equals(real(p), real(q))\
    \ && equals(imag(p), imag(q))) return {p};\n    return {p, q};\n  }\n}\n"
  code: "#include \"base.cpp\"\n#include \"point.cpp\"\n#include \"circle.cpp\"\n\n\
    namespace geometry {\n  // http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=CGL_7_E\n\
    \  Points cross_point_cc(const Circle &c1, const Circle &c2) {\n    Real d = abs(c1.p\
    \ - c2.p), r = c1.r + c2.r;\n    if(sign(d - r) > 0 or sign(d + c1.r - c2.r) <\
    \ 0) return {};\n    Real a = acos((norm(c1.r) - norm(c2.r) + norm(d)) / (2 *\
    \ c1.r * d));\n    Real t = arg(c2.p - c1.p);\n    Point p = c1.p + polar(c1.r,\
    \ t + a);\n    Point q = c1.p + polar(c1.r, t - a);\n    if(equals(real(p), real(q))\
    \ && equals(imag(p), imag(q))) return {p};\n    return {p, q};\n  }\n}\n"
  dependsOn:
  - geometry/base.cpp
  - geometry/point.cpp
  - geometry/circle.cpp
  isVerificationFile: false
  path: geometry/cross_point_cc.cpp
  requiredBy: []
  timestamp: '2020-12-01 17:38:42+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-cgl-7-e.test.cpp
documentation_of: geometry/cross_point_cc.cpp
layout: document
redirect_from:
- /library/geometry/cross_point_cc.cpp
- /library/geometry/cross_point_cc.cpp.html
title: geometry/cross_point_cc.cpp
---
