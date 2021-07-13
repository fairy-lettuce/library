---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-0233.test.cpp
    title: test/verify/aoj-0233.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/convert-base.md
    document_title: "Convert Base(\u9032\u6570\u5909\u63DB)"
    links: []
  bundledCode: "#line 1 \"math/number-theory/convert-base.cpp\"\n/**\n * @brief Convert\
    \ Base(\u9032\u6570\u5909\u63DB)\n * @docs docs/convert-base.md\n */\ntemplate<\
    \ typename T >\nvector< T > convert_base(T x, T b) {\n  vector< T > ret;\n  T\
    \ t = 1, k = abs(b);\n  while(x) {\n    ret.emplace_back((x * t) % k);\n    if(ret.back()\
    \ < 0) ret.back() += k;\n    x -= ret.back() * t;\n    x /= k;\n    t *= b / k;\n\
    \  }\n  if(ret.empty()) ret.emplace_back(0);\n  reverse(begin(ret), end(ret));\n\
    \  return ret;\n}\n"
  code: "/**\n * @brief Convert Base(\u9032\u6570\u5909\u63DB)\n * @docs docs/convert-base.md\n\
    \ */\ntemplate< typename T >\nvector< T > convert_base(T x, T b) {\n  vector<\
    \ T > ret;\n  T t = 1, k = abs(b);\n  while(x) {\n    ret.emplace_back((x * t)\
    \ % k);\n    if(ret.back() < 0) ret.back() += k;\n    x -= ret.back() * t;\n \
    \   x /= k;\n    t *= b / k;\n  }\n  if(ret.empty()) ret.emplace_back(0);\n  reverse(begin(ret),\
    \ end(ret));\n  return ret;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/number-theory/convert-base.cpp
  requiredBy: []
  timestamp: '2021-07-13 21:51:53+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-0233.test.cpp
documentation_of: math/number-theory/convert-base.cpp
layout: document
redirect_from:
- /library/math/number-theory/convert-base.cpp
- /library/math/number-theory/convert-base.cpp.html
title: "Convert Base(\u9032\u6570\u5909\u63DB)"
---
## 概要

10進数 $x$ を $b$ 進数に変換する.

* `convert_base(x, b)`: 10 進数 `x` を `b` 進数に変換した結果を返す.

## 計算量

* $O(\log x)$
