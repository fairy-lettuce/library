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
    path: geometry/cross_point_cl.cpp
    title: geometry/cross_point_cl.cpp
  - icon: ':warning:'
    path: geometry/is_intersect_cs.cpp
    title: geometry/is_intersect_cs.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/line.cpp
    title: geometry/line.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/point.cpp
    title: geometry/point.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/projection.cpp
    title: geometry/projection.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/segment.cpp
    title: geometry/segment.cpp
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
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
    \ < imag(b);\n  }\n\n  using Points = vector< Point >;\n}\n#line 3 \"geometry/line.cpp\"\
    \n\nnamespace geometry {\n  struct Line {\n    Point a, b;\n\n    Line() = default;\n\
    \n    Line(const Point &a, const Point &b) : a(a), b(b) {}\n\n    Line(const Real\
    \ &A, const Real &B, const Real &C) { // Ax+By=C\n      if(equals(A, 0)) {\n \
    \       assert(!equals(B, 0));\n        a = Point(0, C / B);\n        b = Point(1,\
    \ C / B);\n      } else if(equals(B, 0)) {\n        a = Point(C / A, 0);\n   \
    \     b = Point(C / A, 1);\n      } else {\n        a = Point(0, C / B);\n   \
    \     b = Point(C / A, 0);\n      }\n    }\n\n    friend ostream &operator<<(ostream\
    \ &os, Line &l) {\n      return os << l.a << \" to \" << l.b;\n    }\n\n    friend\
    \ istream &operator>>(istream &is, Line &l) {\n      return is >> l.a >> l.b;\n\
    \    }\n  };\n\n  using Lines = vector< Line >;\n}\n#line 3 \"geometry/segment.cpp\"\
    \n\nnamespace geometry {\n  struct Segment : Line {\n    Segment() = default;\n\
    \n    using Line::Line;\n  };\n\n  using Segments = vector< Segment >;\n}\n#line\
    \ 3 \"geometry/circle.cpp\"\n\nnamespace geometry {\n  struct Circle {\n    Point\
    \ p;\n    Real r{};\n\n    Circle() = default;\n\n    Circle(const Point &p, const\
    \ Real &r) : p(p), r(r) {}\n  };\n\n  using Circles = vector< Circle >;\n}\n#line\
    \ 3 \"geometry/projection.cpp\"\n\nnamespace geometry {\n  // http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=CGL_1_A\n\
    \  Point projection(const Line &l, const Point &p) {\n    auto t = dot(p - l.a,\
    \ l.a - l.b) / norm(l.a - l.b);\n    return l.a + (l.a - l.b) * t;\n  }\n}\n#line\
    \ 6 \"geometry/is_intersect_cs.cpp\"\n\nnamespace geometry {\n  int is_intersect_cs(const\
    \ Circle &c, const Segment &l) {\n    Point h = projection(l, c.p);\n    if(sign(norm(h\
    \ - c.p) - norm(c.r)) > 0) return 0;\n    auto d1 = abs(c.p - l.a), d2 = abs(c.p\
    \ - l.b);\n    if(sign(c.r - d1) >= 0 && sign(c.r - d2) >= 0) return 0;\n    if(sign(c.r\
    \ - d1) < 0 && sign(d2 - c.r) > 0 || sign(d1 - c.r) > 0 && sign(c.r - d2) < 0)\
    \ return 1;\n    if(sign(dot(l.a - h, l.b - h)) < 0) return 2;\n    return 0;\n\
    \  }\n}\n#line 3 \"geometry/projection.cpp\"\n\nnamespace geometry {\n  // http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=CGL_1_A\n\
    \  Point projection(const Line &l, const Point &p) {\n    auto t = dot(p - l.a,\
    \ l.a - l.b) / norm(l.a - l.b);\n    return l.a + (l.a - l.b) * t;\n  }\n}\n#line\
    \ 6 \"geometry/cross_point_cl.cpp\"\n\nnamespace geometry {\n  // http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=CGL_7_D\n\
    \  Points cross_point_cl(const Circle &c, const Line &l) {\n    Point pr = projection(l,\
    \ c.p);\n    if(equals(abs(pr - c.p), c.r)) return {pr};\n    Point e = (l.b -\
    \ l.a) / abs(l.b - l.a);\n    auto k = sqrt(norm(c.r) - norm(pr - c.p));\n   \
    \ return {pr - e * k, pr + e * k};\n  }\n}\n#line 6 \"geometry/cross_point_cs.cpp\"\
    \n\nnamespace geometry {\n  Points cross_point_cs(const Circle &c, const Segment\
    \ &s) {\n    int num = is_intersect_cs(c, s);\n    if(num == 0) return {};\n \
    \   if(num == 2) return cross_point_cl(c, s);\n    auto ret = cross_point_cl(c,\
    \ s);\n    if(dot(s.a - ret[0], s.b - ret[0]) > 0) swap(ret[0], ret[1]);\n   \
    \ return {ret[0]};\n  }\n}\n"
  code: "#include \"point.cpp\"\n#include \"segment.cpp\"\n#include \"circle.cpp\"\
    \n#include \"is_intersect_cs.cpp\"\n#include \"cross_point_cl.cpp\"\n\nnamespace\
    \ geometry {\n  Points cross_point_cs(const Circle &c, const Segment &s) {\n \
    \   int num = is_intersect_cs(c, s);\n    if(num == 0) return {};\n    if(num\
    \ == 2) return cross_point_cl(c, s);\n    auto ret = cross_point_cl(c, s);\n \
    \   if(dot(s.a - ret[0], s.b - ret[0]) > 0) swap(ret[0], ret[1]);\n    return\
    \ {ret[0]};\n  }\n}\n"
  dependsOn:
  - geometry/point.cpp
  - geometry/base.cpp
  - geometry/segment.cpp
  - geometry/line.cpp
  - geometry/circle.cpp
  - geometry/is_intersect_cs.cpp
  - geometry/projection.cpp
  - geometry/cross_point_cl.cpp
  isVerificationFile: false
  path: geometry/cross_point_cs.cpp
  requiredBy: []
  timestamp: '2020-12-01 17:38:42+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: geometry/cross_point_cs.cpp
layout: document
redirect_from:
- /library/geometry/cross_point_cs.cpp
- /library/geometry/cross_point_cs.cpp.html
title: geometry/cross_point_cs.cpp
---
