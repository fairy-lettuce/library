---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-discrete-logarithm-mod.test.cpp
    title: test/verify/yosupo-discrete-logarithm-mod.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/mod-log.md
    document_title: "Mod-Log(\u96E2\u6563\u5BFE\u6570\u554F\u984C)"
    links: []
  bundledCode: "#line 1 \"math/combinatorics/mod-log.cpp\"\n/**\n * @brief Mod-Log(\u96E2\
    \u6563\u5BFE\u6570\u554F\u984C)\n * @docs docs/mod-log.md\n */\nint64_t mod_log(int64_t\
    \ a, int64_t b, int64_t p) {\n  int64_t g = 1;\n\n  for(int64_t i = p; i; i /=\
    \ 2) (g *= a) %= p;\n  g = __gcd(g, p);\n\n  int64_t t = 1, c = 0;\n  for(; t\
    \ % g; c++) {\n    if(t == b) return c;\n    (t *= a) %= p;\n  }\n  if(b % g)\
    \ return -1;\n\n  t /= g;\n  b /= g;\n\n  int64_t n = p / g, h = 0, gs = 1;\n\n\
    \  for(; h * h < n; h++) (gs *= a) %= n;\n\n  unordered_map< int64_t, int64_t\
    \ > bs;\n  for(int64_t s = 0, e = b; s < h; bs[e] = ++s) {\n    (e *= a) %= n;\n\
    \  }\n\n  for(int64_t s = 0, e = t; s < n;) {\n    (e *= gs) %= n;\n    s += h;\n\
    \    if(bs.count(e)) return c + s - bs[e];\n  }\n  return -1;\n}\n"
  code: "/**\n * @brief Mod-Log(\u96E2\u6563\u5BFE\u6570\u554F\u984C)\n * @docs docs/mod-log.md\n\
    \ */\nint64_t mod_log(int64_t a, int64_t b, int64_t p) {\n  int64_t g = 1;\n\n\
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
  timestamp: '2020-10-07 20:31:58+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-discrete-logarithm-mod.test.cpp
documentation_of: math/combinatorics/mod-log.cpp
layout: document
redirect_from:
- /library/math/combinatorics/mod-log.cpp
- /library/math/combinatorics/mod-log.cpp.html
title: "Mod-Log(\u96E2\u6563\u5BFE\u6570\u554F\u984C)"
---
## 概要
$a^x \equiv k \pmod b$ を満たす非負整数 $k$ の最小値を求める.

## 使い方

* `mod_log(a, b, p)`: $a^x \equiv k \pmod b$ を満たす非負整数 $k$ の最小値の最小値を返す. ただし, 存在しない場合 $-1$ を返す.

## 計算量

* $O(\sqrt p)$
