---
data:
  _extendedDependsOn:
  - icon: ':question:'
    path: geometry/base.cpp
    title: geometry/base.cpp
  - icon: ':question:'
    path: geometry/point.cpp
    title: geometry/point.cpp
  - icon: ':question:'
    path: geometry/polygon.cpp
    title: geometry/polygon.cpp
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-0412.test.cpp
    title: test/verify/aoj-0412.test.cpp
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
    \ < imag(b);\n  }\n\n  using Points = vector< Point >;\n}\n#line 2 \"geometry/polygon.cpp\"\
    \n\n#line 4 \"geometry/polygon.cpp\"\n\nnamespace geometry {\n  using Polygon\
    \ = vector< Point >;\n  using Polygons = vector< Polygon >;\n}\n#line 4 \"geometry/convex_polygon_contains.cpp\"\
    \n\nnamespace geometry {\n  int convex_polygon_contains(const Polygon &Q, const\
    \ Point &p) {\n    int N = (int) Q.size();\n    Point g = (Q[0] + Q[N / 3] + Q[N\
    \ * 2 / 3]) / 3.0;\n    if(equals(imag(g), imag(p)) && equals(real(g), imag(g)))\
    \ return IN;\n    Point gp = p - g;\n    int l = 0, r = N;\n    while(r - l >\
    \ 1) {\n      int mid = (l + r) / 2;\n      Point gl = Q[l] - g;\n      Point\
    \ gm = Q[mid] - g;\n      if(cross(gl, gm) > 0) {\n        if(cross(gl, gp) >=\
    \ 0 && cross(gm, gp) <= 0) r = mid;\n        else l = mid;\n      } else {\n \
    \       if(cross(gl, gp) <= 0 && cross(gm, gp) >= 0) l = mid;\n        else r\
    \ = mid;\n      }\n    }\n    r %= N;\n    Real v = cross(Q[l] - p, Q[r] - p);\n\
    \    return sign(v) == 0 ? ON : sign(v) == -1 ? OUT : IN;\n  }\n}\n"
  code: "#include \"base.cpp\"\n#include \"point.cpp\"\n#include \"polygon.cpp\"\n\
    \nnamespace geometry {\n  int convex_polygon_contains(const Polygon &Q, const\
    \ Point &p) {\n    int N = (int) Q.size();\n    Point g = (Q[0] + Q[N / 3] + Q[N\
    \ * 2 / 3]) / 3.0;\n    if(equals(imag(g), imag(p)) && equals(real(g), imag(g)))\
    \ return IN;\n    Point gp = p - g;\n    int l = 0, r = N;\n    while(r - l >\
    \ 1) {\n      int mid = (l + r) / 2;\n      Point gl = Q[l] - g;\n      Point\
    \ gm = Q[mid] - g;\n      if(cross(gl, gm) > 0) {\n        if(cross(gl, gp) >=\
    \ 0 && cross(gm, gp) <= 0) r = mid;\n        else l = mid;\n      } else {\n \
    \       if(cross(gl, gp) <= 0 && cross(gm, gp) >= 0) l = mid;\n        else r\
    \ = mid;\n      }\n    }\n    r %= N;\n    Real v = cross(Q[l] - p, Q[r] - p);\n\
    \    return sign(v) == 0 ? ON : sign(v) == -1 ? OUT : IN;\n  }\n}\n"
  dependsOn:
  - geometry/base.cpp
  - geometry/point.cpp
  - geometry/polygon.cpp
  isVerificationFile: false
  path: geometry/convex_polygon_contains.cpp
  requiredBy: []
  timestamp: '2020-12-01 17:38:42+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-0412.test.cpp
documentation_of: geometry/convex_polygon_contains.cpp
layout: document
redirect_from:
- /library/geometry/convex_polygon_contains.cpp
- /library/geometry/convex_polygon_contains.cpp.html
title: geometry/convex_polygon_contains.cpp
---
