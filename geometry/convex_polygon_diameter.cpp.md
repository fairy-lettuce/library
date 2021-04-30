---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: geometry/base.cpp
    title: geometry/base.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/point.cpp
    title: geometry/point.cpp
  - icon: ':heavy_check_mark:'
    path: geometry/polygon.cpp
    title: geometry/polygon.cpp
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-cgl-4-b.test.cpp
    title: test/verify/aoj-cgl-4-b.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links:
    - http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=CGL_4_B
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
    \ = vector< Point >;\n  using Polygons = vector< Polygon >;\n}\n#line 3 \"geometry/convex_polygon_diameter.cpp\"\
    \n\nnamespace geometry {\n  // http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=CGL_4_B\n\
    \  pair< int, int > convex_polygon_diameter(const Polygon &p) {\n    int N = (int)\
    \ p.size();\n    int is = 0, js = 0;\n    for(int i = 1; i < N; i++) {\n     \
    \ if(imag(p[i]) > imag(p[is])) is = i;\n      if(imag(p[i]) < imag(p[js])) js\
    \ = i;\n    }\n    Real maxdis = norm(p[is] - p[js]);\n\n    int maxi, maxj, i,\
    \ j;\n    i = maxi = is;\n    j = maxj = js;\n    do {\n      if(cross(p[(i +\
    \ 1) % N] - p[i], p[(j + 1) % N] - p[j]) >= 0) {\n        j = (j + 1) % N;\n \
    \     } else {\n        i = (i + 1) % N;\n      }\n      if(norm(p[i] - p[j])\
    \ > maxdis) {\n        maxdis = norm(p[i] - p[j]);\n        maxi = i;\n      \
    \  maxj = j;\n      }\n    } while(i != is || j != js);\n    return minmax(maxi,\
    \ maxj);\n  }\n}\n"
  code: "#include \"point.cpp\"\n#include \"polygon.cpp\"\n\nnamespace geometry {\n\
    \  // http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=CGL_4_B\n  pair<\
    \ int, int > convex_polygon_diameter(const Polygon &p) {\n    int N = (int) p.size();\n\
    \    int is = 0, js = 0;\n    for(int i = 1; i < N; i++) {\n      if(imag(p[i])\
    \ > imag(p[is])) is = i;\n      if(imag(p[i]) < imag(p[js])) js = i;\n    }\n\
    \    Real maxdis = norm(p[is] - p[js]);\n\n    int maxi, maxj, i, j;\n    i =\
    \ maxi = is;\n    j = maxj = js;\n    do {\n      if(cross(p[(i + 1) % N] - p[i],\
    \ p[(j + 1) % N] - p[j]) >= 0) {\n        j = (j + 1) % N;\n      } else {\n \
    \       i = (i + 1) % N;\n      }\n      if(norm(p[i] - p[j]) > maxdis) {\n  \
    \      maxdis = norm(p[i] - p[j]);\n        maxi = i;\n        maxj = j;\n   \
    \   }\n    } while(i != is || j != js);\n    return minmax(maxi, maxj);\n  }\n\
    }\n"
  dependsOn:
  - geometry/point.cpp
  - geometry/base.cpp
  - geometry/polygon.cpp
  isVerificationFile: false
  path: geometry/convex_polygon_diameter.cpp
  requiredBy: []
  timestamp: '2020-12-01 17:38:42+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-cgl-4-b.test.cpp
documentation_of: geometry/convex_polygon_diameter.cpp
layout: document
redirect_from:
- /library/geometry/convex_polygon_diameter.cpp
- /library/geometry/convex_polygon_diameter.cpp.html
title: geometry/convex_polygon_diameter.cpp
---
