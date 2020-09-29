---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-dpl-5-g.test.cpp
    title: test/verify/aoj-dpl-5-g.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/bell-number.md
    document_title: "Bell-Number(\u30D9\u30EB\u6570)"
    links: []
  bundledCode: "#line 1 \"math/combinatorics/bell-number.cpp\"\n/**\n * @brief Bell-Number(\u30D9\
    \u30EB\u6570)\n * @docs docs/bell-number.md\n */\ntemplate< typename T >\nT bell_number(int\
    \ n, int k) {\n  if(n == 0) return 1;\n  k = min(k, n);\n  Combination< T > uku(k);\n\
    \  T ret = 0;\n  vector< T > pref(k + 1);\n  pref[0] = 1;\n  for(int i = 1; i\
    \ <= k; i++) {\n    if(i & 1) pref[i] = pref[i - 1] - uku.rfact(i);\n    else\
    \ pref[i] = pref[i - 1] + uku.rfact(i);\n  }\n  for(int i = 1; i <= k; i++) {\n\
    \    ret += T(i).pow(n) * uku.rfact(i) * pref[k - i];\n  }\n  return ret;\n}\n"
  code: "/**\n * @brief Bell-Number(\u30D9\u30EB\u6570)\n * @docs docs/bell-number.md\n\
    \ */\ntemplate< typename T >\nT bell_number(int n, int k) {\n  if(n == 0) return\
    \ 1;\n  k = min(k, n);\n  Combination< T > uku(k);\n  T ret = 0;\n  vector< T\
    \ > pref(k + 1);\n  pref[0] = 1;\n  for(int i = 1; i <= k; i++) {\n    if(i &\
    \ 1) pref[i] = pref[i - 1] - uku.rfact(i);\n    else pref[i] = pref[i - 1] + uku.rfact(i);\n\
    \  }\n  for(int i = 1; i <= k; i++) {\n    ret += T(i).pow(n) * uku.rfact(i) *\
    \ pref[k - i];\n  }\n  return ret;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/combinatorics/bell-number.cpp
  requiredBy: []
  timestamp: '2020-02-24 19:08:02+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-dpl-5-g.test.cpp
documentation_of: math/combinatorics/bell-number.cpp
layout: document
redirect_from:
- /library/math/combinatorics/bell-number.cpp
- /library/math/combinatorics/bell-number.cpp.html
title: "Bell-Number(\u30D9\u30EB\u6570)"
---
## 概要

ベル数 $B(n,k)$ を求める.

区別できる $n$ 個のボールを区別できない $k$ 個以下の箱に分割する方法の数を与える.

特に $B(n,n)$ は $n$ 個のボールを任意個のグループに分割する方法の数である.

* `bell_number(n, k)`: $B(n, k)$ を返す.

## 計算量

* $O(\min(n, k) \log n)$
