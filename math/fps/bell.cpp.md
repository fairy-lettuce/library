---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    _deprecated_at_docs: docs/bell.md
    document_title: "Bell(\u30D9\u30EB\u6570)"
    links: []
  bundledCode: "#line 1 \"math/fps/bell.cpp\"\n/**\n * @brief Bell(\u30D9\u30EB\u6570\
    )\n * @docs docs/bell.md\n */\ntemplate< template< typename > class FPS, typename\
    \ Mint >\nFPS< Mint > bell(int N) {\n  FPS< Mint > poly(N + 1), ret(N + 1);\n\
    \  poly[1] = 1;\n  poly = poly.exp();\n  poly[0] -= 1;\n  poly = poly.exp();\n\
    \  Mint mul = 1;\n  for(int i = 0; i <= N; i++) {\n    ret[i] = poly[i] * mul;\n\
    \    mul *= i + 1;\n  }\n  return ret;\n}\n"
  code: "/**\n * @brief Bell(\u30D9\u30EB\u6570)\n * @docs docs/bell.md\n */\ntemplate<\
    \ template< typename > class FPS, typename Mint >\nFPS< Mint > bell(int N) {\n\
    \  FPS< Mint > poly(N + 1), ret(N + 1);\n  poly[1] = 1;\n  poly = poly.exp();\n\
    \  poly[0] -= 1;\n  poly = poly.exp();\n  Mint mul = 1;\n  for(int i = 0; i <=\
    \ N; i++) {\n    ret[i] = poly[i] * mul;\n    mul *= i + 1;\n  }\n  return ret;\n\
    }\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fps/bell.cpp
  requiredBy: []
  timestamp: '2021-07-14 23:14:04+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: math/fps/bell.cpp
layout: document
redirect_from:
- /library/math/fps/bell.cpp
- /library/math/fps/bell.cpp.html
title: "Bell(\u30D9\u30EB\u6570)"
---
## 概要

ベル数を求める。$n$ 番目(0-indexed) のベル数 $B_n$ は区別できる $n$ 個のボールを任意個のグループに分割する方法の数を与える。

ベル数の母関数 $B(x)$ は以下によって計算される。

$\displaystyle B(x) = \sum_{n=0}^{\infty} B_n \frac {x^n} {n!} = e^{e^x-1}$

## 使い方

* `bell(n)`: $B_0, B_1, \cdots, B_n$ を返す。

## 計算量

* $O(n \log n)$
