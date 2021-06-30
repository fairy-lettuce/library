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
    path: geometry/area.cpp
    title: geometry/area.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/common_area_cp.cpp
    title: geometry/common_area_cp.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/contains.cpp
    title: geometry/contains.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/convex_hull.cpp
    title: geometry/convex_hull.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/convex_polygon_contains.cpp
    title: geometry/convex_polygon_contains.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/convex_polygon_cut.cpp
    title: geometry/convex_polygon_cut.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/convex_polygon_diameter.cpp
    title: geometry/convex_polygon_diameter.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/is_convex_polygon.cpp
    title: geometry/is_convex_polygon.cpp
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-0412.test.cpp
    title: test/verify/aoj-0412.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-cgl-3-a.test.cpp
    title: test/verify/aoj-cgl-3-a.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-cgl-3-b.test.cpp
    title: test/verify/aoj-cgl-3-b.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-cgl-3-c.test.cpp
    title: test/verify/aoj-cgl-3-c.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-cgl-4-a.test.cpp
    title: test/verify/aoj-cgl-4-a.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-cgl-4-b.test.cpp
    title: test/verify/aoj-cgl-4-b.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-cgl-4-c.test.cpp
    title: test/verify/aoj-cgl-4-c.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-cgl-7-h.test.cpp
    title: test/verify/aoj-cgl-7-h.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links: []
  bundledCode: "#line 2 \"geometry/polygon.cpp\"\n\n#line 2 \"geometry/base.cpp\"\n\
    \nnamespace geometry {\n  using Real = double;\n  const Real EPS = 1e-8;\n  const\
    \ Real PI = acos(static_cast< Real >(-1));\n\n  enum {\n    OUT, ON, IN\n  };\n\
    \n  inline int sign(const Real &r) {\n    return r <= -EPS ? -1 : r >= EPS ? 1\
    \ : 0;\n  }\n\n  inline bool equals(const Real &a, const Real &b) {\n    return\
    \ sign(a - b) == 0;\n  }\n}\n#line 3 \"geometry/point.cpp\"\n\nnamespace geometry\
    \ {\n  using Point = complex< Real >;\n\n  istream &operator>>(istream &is, Point\
    \ &p) {\n    Real a, b;\n    is >> a >> b;\n    p = Point(a, b);\n    return is;\n\
    \  }\n\n  ostream &operator<<(ostream &os, const Point &p) {\n    return os <<\
    \ real(p) << \" \" << imag(p);\n  }\n\n  Point operator*(const Point &p, const\
    \ Real &d) {\n    return Point(real(p) * d, imag(p) * d);\n  }\n\n  // rotate\
    \ point p counterclockwise by theta rad\n  Point rotate(Real theta, const Point\
    \ &p) {\n    return Point(cos(theta) * real(p) - sin(theta) * imag(p), sin(theta)\
    \ * real(p) + cos(theta) * imag(p));\n  }\n\n  Real cross(const Point &a, const\
    \ Point &b) {\n    return real(a) * imag(b) - imag(a) * real(b);\n  }\n\n  Real\
    \ dot(const Point &a, const Point &b) {\n    return real(a) * real(b) + imag(a)\
    \ * imag(b);\n  }\n\n  bool compare_x(const Point &a, const Point &b) {\n    return\
    \ equals(real(a), real(b)) ? imag(a) < imag(b) : real(a) < real(b);\n  }\n\n \
    \ bool compare_y(const Point &a, const Point &b) {\n    return equals(imag(a),\
    \ imag(b)) ? real(a) < real(b) : imag(a) < imag(b);\n  }\n\n  using Points = vector<\
    \ Point >;\n}\n#line 4 \"geometry/polygon.cpp\"\n\nnamespace geometry {\n  using\
    \ Polygon = vector< Point >;\n  using Polygons = vector< Polygon >;\n}\n"
  code: "#pragma once\n\n#include \"point.cpp\"\n\nnamespace geometry {\n  using Polygon\
    \ = vector< Point >;\n  using Polygons = vector< Polygon >;\n}\n"
  dependsOn:
  - geometry/point.cpp
  - geometry/base.cpp
  isVerificationFile: false
  path: geometry/polygon.cpp
  requiredBy:
  - geometry/convex_polygon_cut.cpp
  - geometry/convex_polygon_contains.cpp
  - geometry/convex_polygon_diameter.cpp
  - geometry/area.cpp
  - geometry/contains.cpp
  - geometry/is_convex_polygon.cpp
  - geometry/convex_hull.cpp
  - geometry/common_area_cp.cpp
  timestamp: '2020-12-01 17:38:42+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-0412.test.cpp
  - test/verify/aoj-cgl-7-h.test.cpp
  - test/verify/aoj-cgl-3-c.test.cpp
  - test/verify/aoj-cgl-4-b.test.cpp
  - test/verify/aoj-cgl-4-a.test.cpp
  - test/verify/aoj-cgl-3-a.test.cpp
  - test/verify/aoj-cgl-3-b.test.cpp
  - test/verify/aoj-cgl-4-c.test.cpp
documentation_of: geometry/polygon.cpp
layout: document
redirect_from:
- /library/geometry/polygon.cpp
- /library/geometry/polygon.cpp.html
title: geometry/polygon.cpp
---
