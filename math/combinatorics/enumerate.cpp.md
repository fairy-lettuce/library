---
data:
  _extendedDependsOn: []
  _extendedRequiredBy:
  - icon: ':heavy_check_mark:'
    path: math/combinatorics/bell-number.cpp
    title: "Bell-Number(\u30D9\u30EB\u6570)"
  - icon: ':heavy_check_mark:'
    path: math/combinatorics/stirling-number-second.cpp
    title: "Stirling-Number-Second(\u7B2C2\u7A2E\u30B9\u30BF\u30FC\u30EA\u30F3\u30B0\
      \u6570)"
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-dpl-5-g.test.cpp
    title: test/verify/aoj-dpl-5-g.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-dpl-5-i.test.cpp
    title: test/verify/aoj-dpl-5-i.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
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
    \ < 0) return 0;\n    return r == 0 ? 1 : C(n + r - 1, r);\n  }\n};\n"
  code: "template< typename T >\nstruct Enumerate {\nprivate:\n  vector< T > _fact,\
    \ _rfact, _inv;\n\n  inline void expand(size_t sz) {\n    if(_fact.size() < sz\
    \ + 1) {\n      int pre_sz = (int) _fact.size();\n      _fact.resize(sz + 1);\n\
    \      _rfact.resize(sz + 1);\n      _inv.resize(sz + 1);\n      for(int i = pre_sz;\
    \ i <= sz; i++) {\n        _fact[i] = _fact[i - 1] * T(i);\n      }\n      _rfact[sz]\
    \ = T(1) / _fact[sz];\n      for(int i = (int) sz - 1; i >= pre_sz; i--) {\n \
    \       _rfact[i] = _rfact[i + 1] * T(i + 1);\n      }\n      for(int i = pre_sz;\
    \ i <= sz; i++) {\n        _inv[i] = _rfact[i] * _fact[i - 1];\n      }\n    }\n\
    \  }\n\npublic:\n  explicit Enumerate(size_t sz = 0) : _fact{T(1)}, _rfact{T(1)},\
    \ _inv{T(1)} {\n    expand(sz);\n  }\n\n  inline T fact(int k) {\n    expand(k);\n\
    \    return _fact[k];\n  }\n\n  inline T rfact(int k) {\n    expand(k);\n    return\
    \ _rfact[k];\n  }\n\n  inline T inv(int k) {\n    expand(k);\n    return _inv[k];\n\
    \  }\n\n  T P(int n, int r) {\n    if(r < 0 || n < r) return 0;\n    return fact(n)\
    \ * rfact(n - r);\n  }\n\n  T C(int p, int q) {\n    if(q < 0 || p < q) return\
    \ 0;\n    return fact(p) * rfact(q) * rfact(p - q);\n  }\n\n  T H(int n, int r)\
    \ {\n    if(n < 0 || r < 0) return 0;\n    return r == 0 ? 1 : C(n + r - 1, r);\n\
    \  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: math/combinatorics/enumerate.cpp
  requiredBy:
  - math/combinatorics/stirling-number-second.cpp
  - math/combinatorics/bell-number.cpp
  timestamp: '2020-12-16 21:47:02+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-dpl-5-g.test.cpp
  - test/verify/aoj-dpl-5-i.test.cpp
documentation_of: math/combinatorics/enumerate.cpp
layout: document
redirect_from:
- /library/math/combinatorics/enumerate.cpp
- /library/math/combinatorics/enumerate.cpp.html
title: math/combinatorics/enumerate.cpp
---
