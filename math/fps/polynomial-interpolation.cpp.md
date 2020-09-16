---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-polynomial-interpolation.test.cpp
    title: test/verify/yosupo-polynomial-interpolation.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    links: []
  bundledCode: "#line 1 \"math/fps/polynomial-interpolation.cpp\"\ntemplate< class\
    \ T >\nFormalPowerSeries< T > polynomial_interpolation(const FormalPowerSeries<\
    \ T > &xs, const vector< T > &ys) {\n  assert(xs.size() == ys.size());\n  using\
    \ FPS = FormalPowerSeries< T >;\n  PolyBuf< T > buf(xs);\n  FPS w = buf.query(0,\
    \ xs.size()).diff();\n  auto vs = multipoint_evaluation(w, xs, buf);\n  function<\
    \ FPS(int, int) > rec = [&](int l, int r) -> FPS {\n    if(r - l == 1) return\
    \ {ys[l] / vs[l]};\n    int m = (l + r) >> 1;\n    return rec(l, m) * buf.query(m,\
    \ r) + rec(m, r) * buf.query(l, m);\n  };\n  return rec(0, xs.size());\n}\n"
  code: "template< class T >\nFormalPowerSeries< T > polynomial_interpolation(const\
    \ FormalPowerSeries< T > &xs, const vector< T > &ys) {\n  assert(xs.size() ==\
    \ ys.size());\n  using FPS = FormalPowerSeries< T >;\n  PolyBuf< T > buf(xs);\n\
    \  FPS w = buf.query(0, xs.size()).diff();\n  auto vs = multipoint_evaluation(w,\
    \ xs, buf);\n  function< FPS(int, int) > rec = [&](int l, int r) -> FPS {\n  \
    \  if(r - l == 1) return {ys[l] / vs[l]};\n    int m = (l + r) >> 1;\n    return\
    \ rec(l, m) * buf.query(m, r) + rec(m, r) * buf.query(l, m);\n  };\n  return rec(0,\
    \ xs.size());\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fps/polynomial-interpolation.cpp
  requiredBy: []
  timestamp: '2019-11-30 23:36:31+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-polynomial-interpolation.test.cpp
documentation_of: math/fps/polynomial-interpolation.cpp
layout: document
redirect_from:
- /library/math/fps/polynomial-interpolation.cpp
- /library/math/fps/polynomial-interpolation.cpp.html
title: math/fps/polynomial-interpolation.cpp
---
