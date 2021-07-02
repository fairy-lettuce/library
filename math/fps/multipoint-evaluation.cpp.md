---
data:
  _extendedDependsOn: []
  _extendedRequiredBy:
  - icon: ':x:'
    path: math/fps/polynomial-interpolation.cpp
    title: math/fps/polynomial-interpolation.cpp
  _extendedVerifiedWith:
  - icon: ':x:'
    path: test/verify/yosupo-multipoint-evaluation.test.cpp
    title: test/verify/yosupo-multipoint-evaluation.test.cpp
  - icon: ':x:'
    path: test/verify/yosupo-polynomial-interpolation.test.cpp
    title: test/verify/yosupo-polynomial-interpolation.test.cpp
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes:
    links: []
  bundledCode: "#line 1 \"math/fps/multipoint-evaluation.cpp\"\ntemplate< template<\
    \ typename > class FPS, typename Mint >\nstruct PolyBuf {\n  const FPS< Mint >\
    \ xs;\n  using pi = pair< int, int >;\n  map< pi, FPS< Mint > > buf;\n\n  PolyBuf(const\
    \ FPS< Mint > &xs) : xs(xs) {}\n\n  const FPS< Mint > &query(int l, int r) {\n\
    \    if(buf.count({l, r})) return buf[{l, r}];\n    if(l + 1 == r) return buf[{l,\
    \ r}] = {-xs[l], 1};\n    return buf[{l, r}] = query(l, (l + r) >> 1) * query((l\
    \ + r) >> 1, r);\n  }\n};\n\n\ntemplate< template< typename > class FPS, typename\
    \ Mint >\nFPS< Mint > multipoint_evaluation(const FPS< Mint > &as, const FPS<\
    \ Mint > &xs, PolyBuf< FPS, Mint > &buf) {\n  FPS< Mint > ret;\n  const int B\
    \ = 64;\n  function< void(FPS< Mint >, int, int) > rec = [&](FPS< Mint > a, int\
    \ l, int r) -> void {\n    a %= buf.query(l, r);\n    if(a.size() <= B) {\n  \
    \    for(int i = l; i < r; i++) ret.emplace_back(a(xs[i]));\n      return;\n \
    \   }\n    rec(a, l, (l + r) >> 1);\n    rec(a, (l + r) >> 1, r);\n  };\n  rec(as,\
    \ 0, xs.size());\n  return ret;\n};\n\ntemplate< template< typename > class FPS,\
    \ typename Mint >\nFPS< Mint > multipoint_evaluation(const FPS< Mint > &as, const\
    \ FPS< Mint > &xs) {\n  PolyBuf< FPS, Mint > buff(xs);\n  return multipoint_evaluation(as,\
    \ xs, buff);\n}\n\n"
  code: "template< template< typename > class FPS, typename Mint >\nstruct PolyBuf\
    \ {\n  const FPS< Mint > xs;\n  using pi = pair< int, int >;\n  map< pi, FPS<\
    \ Mint > > buf;\n\n  PolyBuf(const FPS< Mint > &xs) : xs(xs) {}\n\n  const FPS<\
    \ Mint > &query(int l, int r) {\n    if(buf.count({l, r})) return buf[{l, r}];\n\
    \    if(l + 1 == r) return buf[{l, r}] = {-xs[l], 1};\n    return buf[{l, r}]\
    \ = query(l, (l + r) >> 1) * query((l + r) >> 1, r);\n  }\n};\n\n\ntemplate< template<\
    \ typename > class FPS, typename Mint >\nFPS< Mint > multipoint_evaluation(const\
    \ FPS< Mint > &as, const FPS< Mint > &xs, PolyBuf< FPS, Mint > &buf) {\n  FPS<\
    \ Mint > ret;\n  const int B = 64;\n  function< void(FPS< Mint >, int, int) >\
    \ rec = [&](FPS< Mint > a, int l, int r) -> void {\n    a %= buf.query(l, r);\n\
    \    if(a.size() <= B) {\n      for(int i = l; i < r; i++) ret.emplace_back(a(xs[i]));\n\
    \      return;\n    }\n    rec(a, l, (l + r) >> 1);\n    rec(a, (l + r) >> 1,\
    \ r);\n  };\n  rec(as, 0, xs.size());\n  return ret;\n};\n\ntemplate< template<\
    \ typename > class FPS, typename Mint >\nFPS< Mint > multipoint_evaluation(const\
    \ FPS< Mint > &as, const FPS< Mint > &xs) {\n  PolyBuf< FPS, Mint > buff(xs);\n\
    \  return multipoint_evaluation(as, xs, buff);\n}\n\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fps/multipoint-evaluation.cpp
  requiredBy:
  - math/fps/polynomial-interpolation.cpp
  timestamp: '2021-07-03 01:50:07+09:00'
  verificationStatus: LIBRARY_ALL_WA
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
