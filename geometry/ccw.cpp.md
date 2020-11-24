---
data:
  _extendedDependsOn:
  - icon: ':question:'
    path: geometry/base.cpp
    title: geometry/base.cpp
  - icon: ':question:'
    path: geometry/point.cpp
    title: geometry/point.cpp
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-cgl-1-c.test.cpp
    title: test/verify/aoj-cgl-1-c.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links:
    - http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=CGL_1_C
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
    \ + imag(a) * imag(b);\n  }\n\n  using Points = vector< Point >;\n}\n#line 2 \"\
    geometry/ccw.cpp\"\n\nnamespace geometry {\n  // http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=CGL_1_C\n\
    \  int ccw(const Point &a, Point b, Point c) {\n    b = b - a, c = c - a;\n  \
    \  if(sign(cross(b, c)) == +1) return +1; // \"COUNTER_CLOCKWISE\"\n    if(sign(cross(b,\
    \ c)) == -1) return -1; // \"CLOCKWISE\"\n    if(sign(dot(b, c)) == -1) return\
    \ +2;   // \"ONLINE_BACK\" c-a-b\n    if(norm(b) < norm(c)) return -2;       //\
    \ \"ONLINE_FRONT\" a-b-c\n    return 0;                              // \"ON_SEGMENT\"\
    \ a-c-b\n  }\n}\n"
  code: "#include \"point.cpp\"\n\nnamespace geometry {\n  // http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=CGL_1_C\n\
    \  int ccw(const Point &a, Point b, Point c) {\n    b = b - a, c = c - a;\n  \
    \  if(sign(cross(b, c)) == +1) return +1; // \"COUNTER_CLOCKWISE\"\n    if(sign(cross(b,\
    \ c)) == -1) return -1; // \"CLOCKWISE\"\n    if(sign(dot(b, c)) == -1) return\
    \ +2;   // \"ONLINE_BACK\" c-a-b\n    if(norm(b) < norm(c)) return -2;       //\
    \ \"ONLINE_FRONT\" a-b-c\n    return 0;                              // \"ON_SEGMENT\"\
    \ a-c-b\n  }\n}\n"
  dependsOn:
  - geometry/point.cpp
  - geometry/base.cpp
  isVerificationFile: false
  path: geometry/ccw.cpp
  requiredBy: []
  timestamp: '2020-11-24 18:23:37+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-cgl-1-c.test.cpp
documentation_of: geometry/ccw.cpp
layout: document
redirect_from:
- /library/geometry/ccw.cpp
- /library/geometry/ccw.cpp.html
title: geometry/ccw.cpp
---
