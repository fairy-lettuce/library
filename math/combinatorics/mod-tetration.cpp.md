---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':x:'
    path: test/verify/yosupo-tetration-mod.test.cpp
    title: test/verify/yosupo-tetration-mod.test.cpp
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes:
    _deprecated_at_docs: docs/mod-tetration.md
    document_title: "Mod-Tetration(\u30C6\u30C8\u30EC\u30FC\u30B7\u30E7\u30F3)"
    links: []
  bundledCode: "#line 1 \"math/combinatorics/mod-tetration.cpp\"\n/**\n * @brief Mod-Tetration(\u30C6\
    \u30C8\u30EC\u30FC\u30B7\u30E7\u30F3)\n * @docs docs/mod-tetration.md\n */\ntemplate<\
    \ typename T >\nT mod_tetration(const T &a, const T &b, const T &m) {\n  if(m\
    \ == 1) return 0;\n  if(a == 0) return !(b & 1);\n  if(b == 0) return 1;\n  if(b\
    \ == 1) return a % m;\n  if(b == 2) return mod_pow(a % m, a, m);\n  auto phi =\
    \ euler_phi(m);\n  return mod_pow(a % m, mod_tetration(a, b - 1, phi) + phi, m);\n\
    }\n"
  code: "/**\n * @brief Mod-Tetration(\u30C6\u30C8\u30EC\u30FC\u30B7\u30E7\u30F3)\n\
    \ * @docs docs/mod-tetration.md\n */\ntemplate< typename T >\nT mod_tetration(const\
    \ T &a, const T &b, const T &m) {\n  if(m == 1) return 0;\n  if(a == 0) return\
    \ !(b & 1);\n  if(b == 0) return 1;\n  if(b == 1) return a % m;\n  if(b == 2)\
    \ return mod_pow(a % m, a, m);\n  auto phi = euler_phi(m);\n  return mod_pow(a\
    \ % m, mod_tetration(a, b - 1, phi) + phi, m);\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/combinatorics/mod-tetration.cpp
  requiredBy: []
  timestamp: '2020-10-07 20:31:58+09:00'
  verificationStatus: LIBRARY_ALL_WA
  verifiedWith:
  - test/verify/yosupo-tetration-mod.test.cpp
documentation_of: math/combinatorics/mod-tetration.cpp
layout: document
redirect_from:
- /library/math/combinatorics/mod-tetration.cpp
- /library/math/combinatorics/mod-tetration.cpp.html
title: "Mod-Tetration(\u30C6\u30C8\u30EC\u30FC\u30B7\u30E7\u30F3)"
---
## 概要
${a \uparrow \uparrow b} \bmod m$ を求める. $\uparrow \uparrow$ はテトレーション演算で $a^{a^{a^{a^{\ldots}}}}$ ($a$ が $b$ 個続く) を指す.

## 使い方

* `mod_tetration(a, b, m)`: ${a \uparrow \uparrow b} \bmod m$ を返す. 

## 計算量

* $O(\sqrt m)$
