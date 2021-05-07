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
    path: geometry/common_area_cp.cpp
    title: geometry/common_area_cp.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/convex_polygon_cut.cpp
    title: geometry/convex_polygon_cut.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/cross_point_cl.cpp
    title: geometry/cross_point_cl.cpp
  - icon: ':warning:'
    path: geometry/cross_point_cs.cpp
    title: geometry/cross_point_cs.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/cross_point_ll.cpp
    title: geometry/cross_point_ll.cpp
  - icon: ':warning:'
    path: geometry/distance_ll.cpp
    title: geometry/distance_ll.cpp
  - icon: ':warning:'
    path: geometry/distance_lp.cpp
    title: geometry/distance_lp.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/distance_sp.cpp
    title: geometry/distance_sp.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/distance_ss.cpp
    title: geometry/distance_ss.cpp
  - icon: ':warning:'
    path: geometry/is_intersect_cl.cpp
    title: geometry/is_intersect_cl.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/is_intersect_cs.cpp
    title: geometry/is_intersect_cs.cpp
  - icon: ':warning:'
    path: geometry/is_intersect_ll.cpp
    title: geometry/is_intersect_ll.cpp
  - icon: ':warning:'
    path: geometry/is_intersect_lp.cpp
    title: geometry/is_intersect_lp.cpp
  - icon: ':warning:'
    path: geometry/is_intersect_ls.cpp
    title: geometry/is_intersect_ls.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/is_intersect_sp.cpp
    title: geometry/is_intersect_sp.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/is_intersect_ss.cpp
    title: geometry/is_intersect_ss.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/is_orthogonal.cpp
    title: geometry/is_orthogonal.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/is_parallel.cpp
    title: geometry/is_parallel.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/projection.cpp
    title: geometry/projection.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/reflection.cpp
    title: geometry/reflection.cpp
  - icon: ':heavy_check_mark:'
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
    path: test/verify/aoj-cgl-2-a.test.cpp
    title: test/verify/aoj-cgl-2-a.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-cgl-2-b.test.cpp
    title: test/verify/aoj-cgl-2-b.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-cgl-2-c.test.cpp
    title: test/verify/aoj-cgl-2-c.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-cgl-2-d.test.cpp
    title: test/verify/aoj-cgl-2-d.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-cgl-4-c.test.cpp
    title: test/verify/aoj-cgl-4-c.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-cgl-7-d.test.cpp
    title: test/verify/aoj-cgl-7-d.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-cgl-7-h.test.cpp
    title: test/verify/aoj-cgl-7-h.test.cpp
  _isVerificationFailed: false
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
    \    }\n  };\n\n  using Lines = vector< Line >;\n}\n"
  code: "#pragma once\n#include \"point.cpp\"\n\nnamespace geometry {\n  struct Line\
    \ {\n    Point a, b;\n\n    Line() = default;\n\n    Line(const Point &a, const\
    \ Point &b) : a(a), b(b) {}\n\n    Line(const Real &A, const Real &B, const Real\
    \ &C) { // Ax+By=C\n      if(equals(A, 0)) {\n        assert(!equals(B, 0));\n\
    \        a = Point(0, C / B);\n        b = Point(1, C / B);\n      } else if(equals(B,\
    \ 0)) {\n        a = Point(C / A, 0);\n        b = Point(C / A, 1);\n      } else\
    \ {\n        a = Point(0, C / B);\n        b = Point(C / A, 0);\n      }\n   \
    \ }\n\n    friend ostream &operator<<(ostream &os, Line &l) {\n      return os\
    \ << l.a << \" to \" << l.b;\n    }\n\n    friend istream &operator>>(istream\
    \ &is, Line &l) {\n      return is >> l.a >> l.b;\n    }\n  };\n\n  using Lines\
    \ = vector< Line >;\n}\n"
  dependsOn:
  - geometry/point.cpp
  - geometry/base.cpp
  isVerificationFile: false
  path: geometry/line.cpp
  requiredBy:
  - geometry/is_intersect_ls.cpp
  - geometry/is_intersect_sp.cpp
  - geometry/is_intersect_cl.cpp
  - geometry/cross_point_cs.cpp
  - geometry/cross_point_ll.cpp
  - geometry/distance_ss.cpp
  - geometry/distance_ll.cpp
  - geometry/is_intersect_ll.cpp
  - geometry/distance_sp.cpp
  - geometry/projection.cpp
  - geometry/is_intersect_cs.cpp
  - geometry/convex_polygon_cut.cpp
  - geometry/cross_point_cl.cpp
  - geometry/is_orthogonal.cpp
  - geometry/common_area_cp.cpp
  - geometry/is_intersect_ss.cpp
  - geometry/distance_lp.cpp
  - geometry/is_intersect_lp.cpp
  - geometry/is_parallel.cpp
  - geometry/segment.cpp
  - geometry/reflection.cpp
  timestamp: '2020-12-01 17:38:42+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-cgl-1-a.test.cpp
  - test/verify/aoj-cgl-2-b.test.cpp
  - test/verify/aoj-cgl-2-d.test.cpp
  - test/verify/aoj-cgl-4-c.test.cpp
  - test/verify/aoj-cgl-2-c.test.cpp
  - test/verify/aoj-cgl-2-a.test.cpp
  - test/verify/aoj-cgl-1-b.test.cpp
  - test/verify/aoj-cgl-7-h.test.cpp
  - test/verify/aoj-cgl-7-d.test.cpp
documentation_of: geometry/line.cpp
layout: document
redirect_from:
- /library/geometry/line.cpp
- /library/geometry/line.cpp.html
title: geometry/line.cpp
---
