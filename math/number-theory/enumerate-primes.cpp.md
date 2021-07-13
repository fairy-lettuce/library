---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: math/number-theory/prime-table.cpp
    title: "Prime-Table(\u7D20\u6570\u30C6\u30FC\u30D6\u30EB)"
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-enumerate-primes.test.cpp
    title: test/verify/yosupo-enumerate-primes.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/enumerate-primes.md
    document_title: "Enumerate Primes(\u7D20\u6570\u5217\u6319)"
    links: []
  bundledCode: "#line 1 \"math/number-theory/prime-table.cpp\"\n/**\n * @brief Prime-Table(\u7D20\
    \u6570\u30C6\u30FC\u30D6\u30EB)\n * @docs docs/prime-table.md\n */\nvector< bool\
    \ > prime_table(int n) {\n  vector< bool > prime(n + 1, true);\n  if(n >= 0) prime[0]\
    \ = false;\n  if(n >= 1) prime[1] = false;\n  for(int i = 2; i * i <= n; i++)\
    \ {\n    if(!prime[i]) continue;\n    for(int j = i * i; j <= n; j += i) {\n \
    \     prime[j] = false;\n    }\n  }\n  return prime;\n}\n#line 2 \"math/number-theory/enumerate-primes.cpp\"\
    \n\n/**\n * @brief Enumerate Primes(\u7D20\u6570\u5217\u6319)\n * @docs docs/enumerate-primes.md\n\
    \ */\nvector< int > enumerate_primes(int n) {\n  if(n <= 1) return {};\n  auto\
    \ d = prime_table(n);\n  vector< int > primes;\n  primes.reserve(count(begin(d),\
    \ end(d), true));\n  for(int i = 0; i < d.size(); i++) {\n    if(d[i]) primes.push_back(i);\n\
    \  }\n  return primes;\n}\n"
  code: "#include \"prime-table.cpp\"\n\n/**\n * @brief Enumerate Primes(\u7D20\u6570\
    \u5217\u6319)\n * @docs docs/enumerate-primes.md\n */\nvector< int > enumerate_primes(int\
    \ n) {\n  if(n <= 1) return {};\n  auto d = prime_table(n);\n  vector< int > primes;\n\
    \  primes.reserve(count(begin(d), end(d), true));\n  for(int i = 0; i < d.size();\
    \ i++) {\n    if(d[i]) primes.push_back(i);\n  }\n  return primes;\n}\n"
  dependsOn:
  - math/number-theory/prime-table.cpp
  isVerificationFile: false
  path: math/number-theory/enumerate-primes.cpp
  requiredBy: []
  timestamp: '2021-07-13 21:51:53+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-enumerate-primes.test.cpp
documentation_of: math/number-theory/enumerate-primes.cpp
layout: document
redirect_from:
- /library/math/number-theory/enumerate-primes.cpp
- /library/math/number-theory/enumerate-primes.cpp.html
title: "Enumerate Primes(\u7D20\u6570\u5217\u6319)"
---
## 概要

エラトステネスの篩により $n$ 以下の全ての素数を列挙する.

## 使い方

* `enumerate_prime(n)`: $n$ 以下の全ての素数を昇順で返す.

## 計算量

* $O(n \log \log n)$
