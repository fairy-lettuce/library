---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: math/combinatorics/enumerate.cpp
    title: math/combinatorics/enumerate.cpp
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
  bundledCode: "#line 1 \"math/combinatorics/enumerate.cpp\"\ntemplate< typename T\
    \ >\nstruct Enumerate {\nprivate:\n  vector< T > _fact, _rfact, _inv;\n\n  inline\
    \ void expand(size_t sz) {\n    if(_fact.size() < sz + 1) {\n      int pre_sz\
    \ = (int) _fact.size();\n      _fact.resize(sz + 1);\n      _rfact.resize(sz +\
    \ 1);\n      _inv.resize(sz + 1);\n      for(int i = pre_sz; i <= sz; i++) {\n\
    \        _fact[i] = _fact[i - 1] * T(i);\n      }\n      _rfact[sz] = T(1) / _fact[sz];\n\
    \      for(int i = (int) sz - 1; i >= pre_sz; i--) {\n        _rfact[i] = _rfact[i\
    \ + 1] * T(i + 1);\n      }\n      for(int i = pre_sz; i <= sz; i++) {\n     \
    \   _inv[i] = _rfact[i] * _fact[i - 1];\n      }\n    }\n  }\n\npublic:\n  explicit\
    \ Enumerate(size_t sz = 0) : _fact{T(1)}, _rfact{T(1)}, _inv{T(1)} {\n    expand(sz);\n\
    \  }\n\n  inline T fact(int k) {\n    expand(k);\n    return _fact[k];\n  }\n\n\
    \  inline T rfact(int k) {\n    expand(k);\n    return _rfact[k];\n  }\n\n  inline\
    \ T inv(int k) {\n    expand(k);\n    return _inv[k];\n  }\n\n  T P(int n, int\
    \ r) {\n    if(r < 0 || n < r) return 0;\n    return fact(n) * rfact(n - r);\n\
    \  }\n\n  T C(int p, int q) {\n    if(q < 0 || p < q) return 0;\n    return fact(p)\
    \ * rfact(q) * rfact(p - q);\n  }\n\n  T H(int n, int r) {\n    if(n < 0 || r\
    \ < 0) return 0;\n    return r == 0 ? 1 : C(n + r - 1, r);\n  }\n};\n#line 2 \"\
    math/combinatorics/bell-number.cpp\"\n\n/**\n * @brief Bell-Number(\u30D9\u30EB\
    \u6570)\n * @docs docs/bell-number.md\n */\ntemplate< typename T >\nT bell_number(int\
    \ n, int k) {\n  if(n == 0) return 1;\n  k = min(k, n);\n  Enumerate< T > uku(k);\n\
    \  T ret = 0;\n  vector< T > pref(k + 1);\n  pref[0] = 1;\n  for(int i = 1; i\
    \ <= k; i++) {\n    if(i & 1) pref[i] = pref[i - 1] - uku.rfact(i);\n    else\
    \ pref[i] = pref[i - 1] + uku.rfact(i);\n  }\n  for(int i = 1; i <= k; i++) {\n\
    \    ret += T(i).pow(n) * uku.rfact(i) * pref[k - i];\n  }\n  return ret;\n}\n"
  code: "#include \"enumerate.cpp\"\n\n/**\n * @brief Bell-Number(\u30D9\u30EB\u6570\
    )\n * @docs docs/bell-number.md\n */\ntemplate< typename T >\nT bell_number(int\
    \ n, int k) {\n  if(n == 0) return 1;\n  k = min(k, n);\n  Enumerate< T > uku(k);\n\
    \  T ret = 0;\n  vector< T > pref(k + 1);\n  pref[0] = 1;\n  for(int i = 1; i\
    \ <= k; i++) {\n    if(i & 1) pref[i] = pref[i - 1] - uku.rfact(i);\n    else\
    \ pref[i] = pref[i - 1] + uku.rfact(i);\n  }\n  for(int i = 1; i <= k; i++) {\n\
    \    ret += T(i).pow(n) * uku.rfact(i) * pref[k - i];\n  }\n  return ret;\n}\n"
  dependsOn:
  - math/combinatorics/enumerate.cpp
  isVerificationFile: false
  path: math/combinatorics/bell-number.cpp
  requiredBy: []
  timestamp: '2020-12-16 21:47:02+09:00'
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
