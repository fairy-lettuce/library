---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-dpl-5-i.test.cpp
    title: test/verify/aoj-dpl-5-i.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/stirling-number-second.md
    document_title: "Stirling-Number-Second(\u7B2C2\u7A2E\u30B9\u30BF\u30FC\u30EA\u30F3\
      \u30B0\u6570)"
    links: []
  bundledCode: "#line 1 \"math/combinatorics/stirling-number-second.cpp\"\n/**\n *\
    \ @brief Stirling-Number-Second(\u7B2C2\u7A2E\u30B9\u30BF\u30FC\u30EA\u30F3\u30B0\
    \u6570)\n * @docs docs/stirling-number-second.md\n */\ntemplate< typename T >\n\
    T stirling_number_second(int n, int k) {\n  Combination< T > table(k);\n  T ret\
    \ = 0;\n  for(int i = 0; i <= k; i++) {\n    auto add = T(i).pow(n) * table.C(k,\
    \ i);\n    if((k - i) & 1) ret -= add;\n    else ret += add;\n  }\n  return ret\
    \ * table.rfact(k);\n}\n\n"
  code: "/**\n * @brief Stirling-Number-Second(\u7B2C2\u7A2E\u30B9\u30BF\u30FC\u30EA\
    \u30F3\u30B0\u6570)\n * @docs docs/stirling-number-second.md\n */\ntemplate< typename\
    \ T >\nT stirling_number_second(int n, int k) {\n  Combination< T > table(k);\n\
    \  T ret = 0;\n  for(int i = 0; i <= k; i++) {\n    auto add = T(i).pow(n) * table.C(k,\
    \ i);\n    if((k - i) & 1) ret -= add;\n    else ret += add;\n  }\n  return ret\
    \ * table.rfact(k);\n}\n\n"
  dependsOn: []
  isVerificationFile: false
  path: math/combinatorics/stirling-number-second.cpp
  requiredBy: []
  timestamp: '2020-11-25 02:37:25+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-dpl-5-i.test.cpp
documentation_of: math/combinatorics/stirling-number-second.cpp
layout: document
redirect_from:
- /library/math/combinatorics/stirling-number-second.cpp
- /library/math/combinatorics/stirling-number-second.cpp.html
title: "Stirling-Number-Second(\u7B2C2\u7A2E\u30B9\u30BF\u30FC\u30EA\u30F3\u30B0\u6570\
  )"
---
## 概要

第 2 種スターリング数 $\\{ {n \atop k} \\}$ を求める.

区別できる $n$ 個のボールを区別できない $k$ 個の箱に分割する方法の数を与える.

計算方法は包除原理の考え方に基づく. $k$ 個の箱のうち空箱があったら違反. 違反する個数で包除する. 具体的には $k$ 個の箱から $k-i$ 個選んだとして, それらの箱にボールを入れない方法の数 $({k \atop i})i^{n}$ を足し引きする.

$\displaystyle \\{ {n \atop k} \\} = { \frac {1}{k!} }  \sum_{i=0}^{k} {(-1)^{k-i} ({k \atop i})i^{n} }$

## 使い方

* `stirling_number_second(n, k)`: $\\{ \textstyle {n \atop k} \\}$ を返す.

## 計算量

* $O(k \log n)$
