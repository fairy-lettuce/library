---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: geometry/base.cpp
    title: geometry/base.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/cross_point_ll.cpp
    title: geometry/cross_point_ll.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/line.cpp
    title: geometry/line.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/point.cpp
    title: geometry/point.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/polygon.cpp
    title: geometry/polygon.cpp
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-cgl-4-c.test.cpp
    title: test/verify/aoj-cgl-4-c.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links:
    - http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=CGL_4_C
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
    \    }\n  };\n\n  using Lines = vector< Line >;\n}\n#line 2 \"geometry/polygon.cpp\"\
    \n\n#line 4 \"geometry/polygon.cpp\"\n\nnamespace geometry {\n  using Polygon\
    \ = vector< Point >;\n  using Polygons = vector< Polygon >;\n}\n#line 3 \"geometry/cross_point_ll.cpp\"\
    \n\nnamespace geometry {\n  Point cross_point_ll(const Line &l, const Line &m)\
    \ {\n    Real A = cross(l.b - l.a, m.b - m.a);\n    Real B = cross(l.b - l.a,\
    \ l.b - m.a);\n    if(equals(abs(A), 0) && equals(abs(B), 0)) return m.a;\n  \
    \  return m.a + (m.b - m.a) * B / A;\n  }\n}\n#line 6 \"geometry/convex_polygon_cut.cpp\"\
    \n\nnamespace geometry {\n  // http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=CGL_4_C\n\
    \  // cut with a straight line l and return a convex polygon on the left\n  Polygon\
    \ convex_polygon_cut(const Polygon &U, const Line &l) {\n    Polygon ret;\n  \
    \  for(int i = 0; i < U.size(); i++) {\n      const Point &now = U[i];\n     \
    \ const Point &nxt = U[(i + 1) % U.size()];\n      auto cf = cross(l.a - now,\
    \ l.b - now);\n      auto cs = cross(l.a - nxt, l.b - nxt);\n      if(sign(cf)\
    \ >= 0) {\n        ret.emplace_back(now);\n      }\n      if(sign(cf) * sign(cs)\
    \ < 0) {\n        ret.emplace_back(cross_point_ll(Line(now, nxt), l));\n     \
    \ }\n    }\n    return ret;\n  }\n}\n"
  code: "#include \"base.cpp\"\n#include \"point.cpp\"\n#include \"line.cpp\"\n#include\
    \ \"polygon.cpp\"\n#include \"cross_point_ll.cpp\"\n\nnamespace geometry {\n \
    \ // http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=CGL_4_C\n  // cut\
    \ with a straight line l and return a convex polygon on the left\n  Polygon convex_polygon_cut(const\
    \ Polygon &U, const Line &l) {\n    Polygon ret;\n    for(int i = 0; i < U.size();\
    \ i++) {\n      const Point &now = U[i];\n      const Point &nxt = U[(i + 1) %\
    \ U.size()];\n      auto cf = cross(l.a - now, l.b - now);\n      auto cs = cross(l.a\
    \ - nxt, l.b - nxt);\n      if(sign(cf) >= 0) {\n        ret.emplace_back(now);\n\
    \      }\n      if(sign(cf) * sign(cs) < 0) {\n        ret.emplace_back(cross_point_ll(Line(now,\
    \ nxt), l));\n      }\n    }\n    return ret;\n  }\n}\n"
  dependsOn:
  - geometry/base.cpp
  - geometry/point.cpp
  - geometry/line.cpp
  - geometry/polygon.cpp
  - geometry/cross_point_ll.cpp
  isVerificationFile: false
  path: geometry/convex_polygon_cut.cpp
  requiredBy: []
  timestamp: '2020-12-01 17:38:42+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-cgl-4-c.test.cpp
documentation_of: geometry/convex_polygon_cut.cpp
layout: document
redirect_from:
- /library/geometry/convex_polygon_cut.cpp
- /library/geometry/convex_polygon_cut.cpp.html
title: geometry/convex_polygon_cut.cpp
---
