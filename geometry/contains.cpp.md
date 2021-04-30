---
data:
  _extendedDependsOn:
  - icon: ':x:'
    path: geometry/base.cpp
    title: geometry/base.cpp
  - icon: ':x:'
    path: geometry/point.cpp
    title: geometry/point.cpp
  - icon: ':x:'
    path: geometry/polygon.cpp
    title: geometry/polygon.cpp
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':x:'
    path: test/verify/aoj-cgl-3-c.test.cpp
    title: test/verify/aoj-cgl-3-c.test.cpp
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes:
    links:
    - http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=CGL_3_C
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
    \ = vector< Point >;\n  using Polygons = vector< Polygon >;\n}\n#line 4 \"geometry/contains.cpp\"\
    \n\nnamespace geometry {\n  // http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=CGL_3_C\n\
    \  int contains(const Polygon &Q, const Point &p) {\n    bool in = false;\n  \
    \  for(int i = 0; i < Q.size(); i++) {\n      Point a = Q[i] - p, b = Q[(i + 1)\
    \ % Q.size()] - p;\n      if(imag(a) > imag(b)) swap(a, b);\n      if(sign(imag(a))\
    \ <= 0 && 0 < sign(imag(b)) && sign(cross(a, b)) < 0) in = !in;\n      if(equals(cross(a,\
    \ b), 0) && sign(dot(a, b)) <= 0) return ON;\n    }\n    return in ? IN : OUT;\n\
    \  }\n}\n"
  code: "#include \"base.cpp\"\n#include \"point.cpp\"\n#include \"polygon.cpp\"\n\
    \nnamespace geometry {\n  // http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=CGL_3_C\n\
    \  int contains(const Polygon &Q, const Point &p) {\n    bool in = false;\n  \
    \  for(int i = 0; i < Q.size(); i++) {\n      Point a = Q[i] - p, b = Q[(i + 1)\
    \ % Q.size()] - p;\n      if(imag(a) > imag(b)) swap(a, b);\n      if(sign(imag(a))\
    \ <= 0 && 0 < sign(imag(b)) && sign(cross(a, b)) < 0) in = !in;\n      if(equals(cross(a,\
    \ b), 0) && sign(dot(a, b)) <= 0) return ON;\n    }\n    return in ? IN : OUT;\n\
    \  }\n}\n"
  dependsOn:
  - geometry/base.cpp
  - geometry/point.cpp
  - geometry/polygon.cpp
  isVerificationFile: false
  path: geometry/contains.cpp
  requiredBy: []
  timestamp: '2020-12-01 17:38:42+09:00'
  verificationStatus: LIBRARY_ALL_WA
  verifiedWith:
  - test/verify/aoj-cgl-3-c.test.cpp
documentation_of: geometry/contains.cpp
layout: document
redirect_from:
- /library/geometry/contains.cpp
- /library/geometry/contains.cpp.html
title: geometry/contains.cpp
---
