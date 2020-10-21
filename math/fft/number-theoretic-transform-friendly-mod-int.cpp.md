---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-bellnoulli-number.test.cpp
    title: test/verify/yosupo-bellnoulli-number.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-exp-of-formal-power-series.test.cpp
    title: test/verify/yosupo-exp-of-formal-power-series.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-inv-of-formal-power-series.test.cpp
    title: test/verify/yosupo-inv-of-formal-power-series.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-log-of-formal-power-series.test.cpp
    title: test/verify/yosupo-log-of-formal-power-series.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-multipoint-evaluation.test.cpp
    title: test/verify/yosupo-multipoint-evaluation.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-partition-function.test.cpp
    title: test/verify/yosupo-partition-function.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-polynomial-interpolation.test.cpp
    title: test/verify/yosupo-polynomial-interpolation.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-sqrt-of-formal-power-series.test.cpp
    title: test/verify/yosupo-sqrt-of-formal-power-series.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links: []
  bundledCode: "#line 1 \"math/fft/number-theoretic-transform-friendly-mod-int.cpp\"\
    \ntemplate< typename Mint >\nstruct NumberTheoreticTransformFriendlyModInt {\n\
    \n  vector< Mint > dw, idw;\n  int max_base;\n  Mint root;\n\n  NumberTheoreticTransformFriendlyModInt()\
    \ {\n    const unsigned mod = Mint::get_mod();\n    assert(mod >= 3 && mod % 2\
    \ == 1);\n    auto tmp = mod - 1;\n    max_base = 0;\n    while(tmp % 2 == 0)\
    \ tmp >>= 1, max_base++;\n    root = 2;\n    while(root.pow((mod - 1) >> 1) ==\
    \ 1) root += 1;\n    assert(root.pow(mod - 1) == 1);\n    dw.resize(max_base);\n\
    \    idw.resize(max_base);\n    for(int i = 0; i < max_base; i++) {\n      dw[i]\
    \ = -root.pow((mod - 1) >> (i + 2));\n      idw[i] = Mint(1) / dw[i];\n    }\n\
    \  }\n\n  void ntt(vector< Mint > &a) {\n    const int n = (int) a.size();\n \
    \   assert((n & (n - 1)) == 0);\n    assert(__builtin_ctz(n) <= max_base);\n \
    \   for(int m = n; m >>= 1;) {\n      Mint w = 1;\n      for(int s = 0, k = 0;\
    \ s < n; s += 2 * m) {\n        for(int i = s, j = s + m; i < s + m; ++i, ++j)\
    \ {\n          auto x = a[i], y = a[j] * w;\n          a[i] = x + y, a[j] = x\
    \ - y;\n        }\n        w *= dw[__builtin_ctz(++k)];\n      }\n    }\n  }\n\
    \n  void intt(vector< Mint > &a, bool f = true) {\n    const int n = (int) a.size();\n\
    \    assert((n & (n - 1)) == 0);\n    assert(__builtin_ctz(n) <= max_base);\n\
    \    for(int m = 1; m < n; m *= 2) {\n      Mint w = 1;\n      for(int s = 0,\
    \ k = 0; s < n; s += 2 * m) {\n        for(int i = s, j = s + m; i < s + m; ++i,\
    \ ++j) {\n          auto x = a[i], y = a[j];\n          a[i] = x + y, a[j] = (x\
    \ - y) * w;\n        }\n        w *= idw[__builtin_ctz(++k)];\n      }\n    }\n\
    \    if(f) {\n      Mint inv_sz = Mint(1) / n;\n      for(int i = 0; i < n; i++)\
    \ a[i] *= inv_sz;\n    }\n  }\n\n  vector< Mint > multiply(vector< Mint > a, vector<\
    \ Mint > b) {\n    int need = a.size() + b.size() - 1;\n    int nbase = 1;\n \
    \   while((1 << nbase) < need) nbase++;\n    int sz = 1 << nbase;\n    a.resize(sz,\
    \ 0);\n    b.resize(sz, 0);\n    ntt(a);\n    ntt(b);\n    Mint inv_sz = Mint(1)\
    \ / sz;\n    for(int i = 0; i < sz; i++) a[i] *= b[i] * inv_sz;\n    intt(a, false);\n\
    \    a.resize(need);\n    return a;\n  }\n};\n"
  code: "template< typename Mint >\nstruct NumberTheoreticTransformFriendlyModInt\
    \ {\n\n  vector< Mint > dw, idw;\n  int max_base;\n  Mint root;\n\n  NumberTheoreticTransformFriendlyModInt()\
    \ {\n    const unsigned mod = Mint::get_mod();\n    assert(mod >= 3 && mod % 2\
    \ == 1);\n    auto tmp = mod - 1;\n    max_base = 0;\n    while(tmp % 2 == 0)\
    \ tmp >>= 1, max_base++;\n    root = 2;\n    while(root.pow((mod - 1) >> 1) ==\
    \ 1) root += 1;\n    assert(root.pow(mod - 1) == 1);\n    dw.resize(max_base);\n\
    \    idw.resize(max_base);\n    for(int i = 0; i < max_base; i++) {\n      dw[i]\
    \ = -root.pow((mod - 1) >> (i + 2));\n      idw[i] = Mint(1) / dw[i];\n    }\n\
    \  }\n\n  void ntt(vector< Mint > &a) {\n    const int n = (int) a.size();\n \
    \   assert((n & (n - 1)) == 0);\n    assert(__builtin_ctz(n) <= max_base);\n \
    \   for(int m = n; m >>= 1;) {\n      Mint w = 1;\n      for(int s = 0, k = 0;\
    \ s < n; s += 2 * m) {\n        for(int i = s, j = s + m; i < s + m; ++i, ++j)\
    \ {\n          auto x = a[i], y = a[j] * w;\n          a[i] = x + y, a[j] = x\
    \ - y;\n        }\n        w *= dw[__builtin_ctz(++k)];\n      }\n    }\n  }\n\
    \n  void intt(vector< Mint > &a, bool f = true) {\n    const int n = (int) a.size();\n\
    \    assert((n & (n - 1)) == 0);\n    assert(__builtin_ctz(n) <= max_base);\n\
    \    for(int m = 1; m < n; m *= 2) {\n      Mint w = 1;\n      for(int s = 0,\
    \ k = 0; s < n; s += 2 * m) {\n        for(int i = s, j = s + m; i < s + m; ++i,\
    \ ++j) {\n          auto x = a[i], y = a[j];\n          a[i] = x + y, a[j] = (x\
    \ - y) * w;\n        }\n        w *= idw[__builtin_ctz(++k)];\n      }\n    }\n\
    \    if(f) {\n      Mint inv_sz = Mint(1) / n;\n      for(int i = 0; i < n; i++)\
    \ a[i] *= inv_sz;\n    }\n  }\n\n  vector< Mint > multiply(vector< Mint > a, vector<\
    \ Mint > b) {\n    int need = a.size() + b.size() - 1;\n    int nbase = 1;\n \
    \   while((1 << nbase) < need) nbase++;\n    int sz = 1 << nbase;\n    a.resize(sz,\
    \ 0);\n    b.resize(sz, 0);\n    ntt(a);\n    ntt(b);\n    Mint inv_sz = Mint(1)\
    \ / sz;\n    for(int i = 0; i < sz; i++) a[i] *= b[i] * inv_sz;\n    intt(a, false);\n\
    \    a.resize(need);\n    return a;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fft/number-theoretic-transform-friendly-mod-int.cpp
  requiredBy: []
  timestamp: '2020-02-24 19:19:55+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-multipoint-evaluation.test.cpp
  - test/verify/yosupo-polynomial-interpolation.test.cpp
  - test/verify/yosupo-log-of-formal-power-series.test.cpp
  - test/verify/yosupo-inv-of-formal-power-series.test.cpp
  - test/verify/yosupo-exp-of-formal-power-series.test.cpp
  - test/verify/yosupo-partition-function.test.cpp
  - test/verify/yosupo-bellnoulli-number.test.cpp
  - test/verify/yosupo-sqrt-of-formal-power-series.test.cpp
documentation_of: math/fft/number-theoretic-transform-friendly-mod-int.cpp
layout: document
redirect_from:
- /library/math/fft/number-theoretic-transform-friendly-mod-int.cpp
- /library/math/fft/number-theoretic-transform-friendly-mod-int.cpp.html
title: math/fft/number-theoretic-transform-friendly-mod-int.cpp
---
