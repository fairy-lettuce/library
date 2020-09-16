---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-dpl-5-i.test.cpp
    title: test/verify/aoj-dpl-5-i.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-dpl-5-g.test.cpp
    title: test/verify/aoj-dpl-5-g.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    links: []
  bundledCode: "#line 1 \"math/combinatorics/combination.cpp\"\ntemplate< typename\
    \ T >\nstruct Combination {\n  vector< T > _fact, _rfact, _inv;\n\n  Combination(int\
    \ sz) : _fact(sz + 1), _rfact(sz + 1), _inv(sz + 1) {\n    _fact[0] = _rfact[sz]\
    \ = _inv[0] = 1;\n    for(int i = 1; i <= sz; i++) _fact[i] = _fact[i - 1] * i;\n\
    \    _rfact[sz] /= _fact[sz];\n    for(int i = sz - 1; i >= 0; i--) _rfact[i]\
    \ = _rfact[i + 1] * (i + 1);\n    for(int i = 1; i <= sz; i++) _inv[i] = _rfact[i]\
    \ * _fact[i - 1];\n  }\n\n  inline T fact(int k) const { return _fact[k]; }\n\n\
    \  inline T rfact(int k) const { return _rfact[k]; }\n\n  inline T inv(int k)\
    \ const { return _inv[k]; }\n\n  T P(int n, int r) const {\n    if(r < 0 || n\
    \ < r) return 0;\n    return fact(n) * rfact(n - r);\n  }\n\n  T C(int p, int\
    \ q) const {\n    if(q < 0 || p < q) return 0;\n    return fact(p) * rfact(q)\
    \ * rfact(p - q);\n  }\n\n  T H(int n, int r) const {\n    if(n < 0 || r < 0)\
    \ return (0);\n    return r == 0 ? 1 : C(n + r - 1, r);\n  }\n};\n"
  code: "template< typename T >\nstruct Combination {\n  vector< T > _fact, _rfact,\
    \ _inv;\n\n  Combination(int sz) : _fact(sz + 1), _rfact(sz + 1), _inv(sz + 1)\
    \ {\n    _fact[0] = _rfact[sz] = _inv[0] = 1;\n    for(int i = 1; i <= sz; i++)\
    \ _fact[i] = _fact[i - 1] * i;\n    _rfact[sz] /= _fact[sz];\n    for(int i =\
    \ sz - 1; i >= 0; i--) _rfact[i] = _rfact[i + 1] * (i + 1);\n    for(int i = 1;\
    \ i <= sz; i++) _inv[i] = _rfact[i] * _fact[i - 1];\n  }\n\n  inline T fact(int\
    \ k) const { return _fact[k]; }\n\n  inline T rfact(int k) const { return _rfact[k];\
    \ }\n\n  inline T inv(int k) const { return _inv[k]; }\n\n  T P(int n, int r)\
    \ const {\n    if(r < 0 || n < r) return 0;\n    return fact(n) * rfact(n - r);\n\
    \  }\n\n  T C(int p, int q) const {\n    if(q < 0 || p < q) return 0;\n    return\
    \ fact(p) * rfact(q) * rfact(p - q);\n  }\n\n  T H(int n, int r) const {\n   \
    \ if(n < 0 || r < 0) return (0);\n    return r == 0 ? 1 : C(n + r - 1, r);\n \
    \ }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: math/combinatorics/combination.cpp
  requiredBy: []
  timestamp: '2019-11-30 23:36:31+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-dpl-5-i.test.cpp
  - test/verify/aoj-dpl-5-g.test.cpp
documentation_of: math/combinatorics/combination.cpp
layout: document
redirect_from:
- /library/math/combinatorics/combination.cpp
- /library/math/combinatorics/combination.cpp.html
title: math/combinatorics/combination.cpp
---
