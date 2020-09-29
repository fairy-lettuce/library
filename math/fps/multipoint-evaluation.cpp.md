---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-multipoint-evaluation.test.cpp
    title: test/verify/yosupo-multipoint-evaluation.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-polynomial-interpolation.test.cpp
    title: test/verify/yosupo-polynomial-interpolation.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links: []
  bundledCode: "#line 1 \"math/fps/multipoint-evaluation.cpp\"\ntemplate< typename\
    \ T >\nstruct PolyBuf {\n  using FPS = FormalPowerSeries< T >;\n  const FPS xs;\n\
    \  using pi = pair< int, int >;\n  map< pi, FPS > buf;\n\n  PolyBuf(const FPS\
    \ &xs) : xs(xs) {}\n\n  const FPS &query(int l, int r) {\n    if(buf.count({l,\
    \ r})) return buf[{l, r}];\n    if(l + 1 == r) return buf[{l, r}] = {-xs[l], 1};\n\
    \    return buf[{l, r}] = query(l, (l + r) >> 1) * query((l + r) >> 1, r);\n \
    \ }\n};\n\n\ntemplate< typename T >\nFormalPowerSeries< T > multipoint_evaluation(const\
    \ FormalPowerSeries< T > &as, const FormalPowerSeries< T > &xs, PolyBuf< T > &buf)\
    \ {\n  using FPS = FormalPowerSeries< T >;\n  FPS ret;\n  const int B = 64;\n\
    \  function< void(FPS, int, int) > rec = [&](FPS a, int l, int r) -> void {\n\
    \    a %= buf.query(l, r);\n    if(a.size() <= B) {\n      for(int i = l; i <\
    \ r; i++) ret.emplace_back(a.eval(xs[i]));\n      return;\n    }\n    rec(a, l,\
    \ (l + r) >> 1);\n    rec(a, (l + r) >> 1, r);\n  };\n  rec(as, 0, xs.size());\n\
    \  return ret;\n};\n\ntemplate< typename T >\nFormalPowerSeries< T > multipoint_evaluation(const\
    \ FormalPowerSeries< T > &as, const FormalPowerSeries< T > &xs) {\n  PolyBuf<\
    \ T > buff(xs);\n  return multipoint_evaluation(as, xs, buff);\n}\n\n"
  code: "template< typename T >\nstruct PolyBuf {\n  using FPS = FormalPowerSeries<\
    \ T >;\n  const FPS xs;\n  using pi = pair< int, int >;\n  map< pi, FPS > buf;\n\
    \n  PolyBuf(const FPS &xs) : xs(xs) {}\n\n  const FPS &query(int l, int r) {\n\
    \    if(buf.count({l, r})) return buf[{l, r}];\n    if(l + 1 == r) return buf[{l,\
    \ r}] = {-xs[l], 1};\n    return buf[{l, r}] = query(l, (l + r) >> 1) * query((l\
    \ + r) >> 1, r);\n  }\n};\n\n\ntemplate< typename T >\nFormalPowerSeries< T >\
    \ multipoint_evaluation(const FormalPowerSeries< T > &as, const FormalPowerSeries<\
    \ T > &xs, PolyBuf< T > &buf) {\n  using FPS = FormalPowerSeries< T >;\n  FPS\
    \ ret;\n  const int B = 64;\n  function< void(FPS, int, int) > rec = [&](FPS a,\
    \ int l, int r) -> void {\n    a %= buf.query(l, r);\n    if(a.size() <= B) {\n\
    \      for(int i = l; i < r; i++) ret.emplace_back(a.eval(xs[i]));\n      return;\n\
    \    }\n    rec(a, l, (l + r) >> 1);\n    rec(a, (l + r) >> 1, r);\n  };\n  rec(as,\
    \ 0, xs.size());\n  return ret;\n};\n\ntemplate< typename T >\nFormalPowerSeries<\
    \ T > multipoint_evaluation(const FormalPowerSeries< T > &as, const FormalPowerSeries<\
    \ T > &xs) {\n  PolyBuf< T > buff(xs);\n  return multipoint_evaluation(as, xs,\
    \ buff);\n}\n\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fps/multipoint-evaluation.cpp
  requiredBy: []
  timestamp: '2019-11-30 23:36:31+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-multipoint-evaluation.test.cpp
  - test/verify/yosupo-polynomial-interpolation.test.cpp
documentation_of: math/fps/multipoint-evaluation.cpp
layout: document
redirect_from:
- /library/math/fps/multipoint-evaluation.cpp
- /library/math/fps/multipoint-evaluation.cpp.html
title: math/fps/multipoint-evaluation.cpp
---
