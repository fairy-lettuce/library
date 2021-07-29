---
data:
  _extendedDependsOn: []
  _extendedRequiredBy:
  - icon: ':heavy_check_mark:'
    path: math/number-theory/prime-count.cpp
    title: "Prime Count(\u7D20\u6570\u306E\u500B\u6570)"
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-counting-primes.test.cpp
    title: test/verify/yosupo-counting-primes.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-kth-root-integer.test.cpp
    title: test/verify/yosupo-kth-root-integer.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/kth-root-integer.md
    document_title: Kth Root Integer
    links: []
  bundledCode: "#line 1 \"math/number-theory/kth-root-integer.cpp\"\n/**\n * @brief\
    \ Kth Root Integer\n * @docs docs/kth-root-integer.md\n */\nuint64_t kth_root_integer(uint64_t\
    \ a, int k) {\n  if(k == 1) return a;\n  auto check = [&](uint32_t x) {\n    uint64_t\
    \ mul = 1;\n    for(int j = 0; j < k; j++) {\n      if(__builtin_mul_overflow(mul,\
    \ x, &mul)) return false;\n    }\n    return mul <= a;\n  };\n  uint64_t ret =\
    \ 0;\n  for(int i = 31; i >= 0; i--) {\n    if(check(ret | (1u << i))) ret |=\
    \ 1u << i;\n  }\n  return ret;\n}\n"
  code: "/**\n * @brief Kth Root Integer\n * @docs docs/kth-root-integer.md\n */\n\
    uint64_t kth_root_integer(uint64_t a, int k) {\n  if(k == 1) return a;\n  auto\
    \ check = [&](uint32_t x) {\n    uint64_t mul = 1;\n    for(int j = 0; j < k;\
    \ j++) {\n      if(__builtin_mul_overflow(mul, x, &mul)) return false;\n    }\n\
    \    return mul <= a;\n  };\n  uint64_t ret = 0;\n  for(int i = 31; i >= 0; i--)\
    \ {\n    if(check(ret | (1u << i))) ret |= 1u << i;\n  }\n  return ret;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/number-theory/kth-root-integer.cpp
  requiredBy:
  - math/number-theory/prime-count.cpp
  timestamp: '2021-07-17 00:36:52+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-counting-primes.test.cpp
  - test/verify/yosupo-kth-root-integer.test.cpp
documentation_of: math/number-theory/kth-root-integer.cpp
layout: document
redirect_from:
- /library/math/number-theory/kth-root-integer.cpp
- /library/math/number-theory/kth-root-integer.cpp.html
title: Kth Root Integer
---
## 概要

$a$ と $k$ が与えられたとき, $\textrm{floor}{(a^{\frac {1} {k}})}$ を求める.

## 使い方

* `kth_root(a, k)`: $\textrm{floor}{(a^{\frac {1} {k}})}$ を返す.

## 計算量

* $O(k \log a)$
