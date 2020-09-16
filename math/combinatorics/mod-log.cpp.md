---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-discrete-logarithm-mod.test.cpp
    title: test/verify/yosupo-discrete-logarithm-mod.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    links: []
  bundledCode: "#line 1 \"math/combinatorics/mod-log.cpp\"\nint64_t mod_log(int64_t\
    \ a, int64_t b, int64_t p) {\n  int64_t g = 1;\n\n  for(int64_t i = p; i; i /=\
    \ 2) (g *= a) %= p;\n  g = __gcd(g, p);\n\n  int64_t t = 1, c = 0;\n  for(; t\
    \ % g; c++) {\n    if(t == b) return c;\n    (t *= a) %= p;\n  }\n  if(b % g)\
    \ return -1;\n\n  t /= g;\n  b /= g;\n\n  int64_t n = p / g, h = 0, gs = 1;\n\n\
    \  for(; h * h < n; h++) (gs *= a) %= n;\n\n  unordered_map< int64_t, int64_t\
    \ > bs;\n  for(int64_t s = 0, e = b; s < h; bs[e] = ++s) {\n    (e *= a) %= n;\n\
    \  }\n\n  for(int64_t s = 0, e = t; s < n;) {\n    (e *= gs) %= n;\n    s += h;\n\
    \    if(bs.count(e)) return c + s - bs[e];\n  }\n  return -1;\n}\n"
  code: "int64_t mod_log(int64_t a, int64_t b, int64_t p) {\n  int64_t g = 1;\n\n\
    \  for(int64_t i = p; i; i /= 2) (g *= a) %= p;\n  g = __gcd(g, p);\n\n  int64_t\
    \ t = 1, c = 0;\n  for(; t % g; c++) {\n    if(t == b) return c;\n    (t *= a)\
    \ %= p;\n  }\n  if(b % g) return -1;\n\n  t /= g;\n  b /= g;\n\n  int64_t n =\
    \ p / g, h = 0, gs = 1;\n\n  for(; h * h < n; h++) (gs *= a) %= n;\n\n  unordered_map<\
    \ int64_t, int64_t > bs;\n  for(int64_t s = 0, e = b; s < h; bs[e] = ++s) {\n\
    \    (e *= a) %= n;\n  }\n\n  for(int64_t s = 0, e = t; s < n;) {\n    (e *= gs)\
    \ %= n;\n    s += h;\n    if(bs.count(e)) return c + s - bs[e];\n  }\n  return\
    \ -1;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/combinatorics/mod-log.cpp
  requiredBy: []
  timestamp: '2019-11-30 23:36:31+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-discrete-logarithm-mod.test.cpp
documentation_of: math/combinatorics/mod-log.cpp
layout: document
redirect_from:
- /library/math/combinatorics/mod-log.cpp
- /library/math/combinatorics/mod-log.cpp.html
title: math/combinatorics/mod-log.cpp
---
