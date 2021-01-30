---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-convolution-mod.test.cpp
    title: test/verify/yosupo-convolution-mod.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links: []
  bundledCode: "#line 1 \"math/fft/number-theoretic-transform.cpp\"\ntemplate< int\
    \ mod >\nstruct NumberTheoreticTransform {\n\n  vector< int > rev, rts;\n  int\
    \ base, max_base, root;\n\n  NumberTheoreticTransform() : base(1), rev{0, 1},\
    \ rts{0, 1} {\n    assert(mod >= 3 && mod % 2 == 1);\n    auto tmp = mod - 1;\n\
    \    max_base = 0;\n    while(tmp % 2 == 0) tmp >>= 1, max_base++;\n    root =\
    \ 2;\n    while(mod_pow(root, (mod - 1) >> 1) == 1) ++root;\n    assert(mod_pow(root,\
    \ mod - 1) == 1);\n    root = mod_pow(root, (mod - 1) >> max_base);\n  }\n\n \
    \ inline int mod_pow(int x, int n) {\n    int ret = 1;\n    while(n > 0) {\n \
    \     if(n & 1) ret = mul(ret, x);\n      x = mul(x, x);\n      n >>= 1;\n   \
    \ }\n    return ret;\n  }\n\n  inline int inverse(int x) {\n    return mod_pow(x,\
    \ mod - 2);\n  }\n\n  inline unsigned add(unsigned x, unsigned y) {\n    x +=\
    \ y;\n    if(x >= mod) x -= mod;\n    return x;\n  }\n\n  inline unsigned mul(unsigned\
    \ a, unsigned b) {\n    return 1ull * a * b % (unsigned long long) mod;\n  }\n\
    \n  void ensure_base(int nbase) {\n    if(nbase <= base) return;\n    rev.resize(1\
    \ << nbase);\n    rts.resize(1 << nbase);\n    for(int i = 0; i < (1 << nbase);\
    \ i++) {\n      rev[i] = (rev[i >> 1] >> 1) + ((i & 1) << (nbase - 1));\n    }\n\
    \    assert(nbase <= max_base);\n    while(base < nbase) {\n      int z = mod_pow(root,\
    \ 1 << (max_base - 1 - base));\n      for(int i = 1 << (base - 1); i < (1 << base);\
    \ i++) {\n        rts[i << 1] = rts[i];\n        rts[(i << 1) + 1] = mul(rts[i],\
    \ z);\n      }\n      ++base;\n    }\n  }\n\n  void ntt(vector< int > &a) {\n\
    \    const int n = (int) a.size();\n    assert((n & (n - 1)) == 0);\n    int zeros\
    \ = __builtin_ctz(n);\n    ensure_base(zeros);\n    int shift = base - zeros;\n\
    \    for(int i = 0; i < n; i++) {\n      if(i < (rev[i] >> shift)) {\n       \
    \ swap(a[i], a[rev[i] >> shift]);\n      }\n    }\n    for(int k = 1; k < n; k\
    \ <<= 1) {\n      for(int i = 0; i < n; i += 2 * k) {\n        for(int j = 0;\
    \ j < k; j++) {\n          int z = mul(a[i + j + k], rts[j + k]);\n          a[i\
    \ + j + k] = add(a[i + j], mod - z);\n          a[i + j] = add(a[i + j], z);\n\
    \        }\n      }\n    }\n  }\n\n  vector< int > multiply(vector< int > a, vector<\
    \ int > b) {\n    int need = a.size() + b.size() - 1;\n    int nbase = 1;\n  \
    \  while((1 << nbase) < need) nbase++;\n    ensure_base(nbase);\n    int sz =\
    \ 1 << nbase;\n    a.resize(sz, 0);\n    b.resize(sz, 0);\n    ntt(a);\n    ntt(b);\n\
    \    int inv_sz = inverse(sz);\n    for(int i = 0; i < sz; i++) {\n      a[i]\
    \ = mul(a[i], mul(b[i], inv_sz));\n    }\n    reverse(a.begin() + 1, a.end());\n\
    \    ntt(a);\n    a.resize(need);\n    return a;\n  }\n};\n"
  code: "template< int mod >\nstruct NumberTheoreticTransform {\n\n  vector< int >\
    \ rev, rts;\n  int base, max_base, root;\n\n  NumberTheoreticTransform() : base(1),\
    \ rev{0, 1}, rts{0, 1} {\n    assert(mod >= 3 && mod % 2 == 1);\n    auto tmp\
    \ = mod - 1;\n    max_base = 0;\n    while(tmp % 2 == 0) tmp >>= 1, max_base++;\n\
    \    root = 2;\n    while(mod_pow(root, (mod - 1) >> 1) == 1) ++root;\n    assert(mod_pow(root,\
    \ mod - 1) == 1);\n    root = mod_pow(root, (mod - 1) >> max_base);\n  }\n\n \
    \ inline int mod_pow(int x, int n) {\n    int ret = 1;\n    while(n > 0) {\n \
    \     if(n & 1) ret = mul(ret, x);\n      x = mul(x, x);\n      n >>= 1;\n   \
    \ }\n    return ret;\n  }\n\n  inline int inverse(int x) {\n    return mod_pow(x,\
    \ mod - 2);\n  }\n\n  inline unsigned add(unsigned x, unsigned y) {\n    x +=\
    \ y;\n    if(x >= mod) x -= mod;\n    return x;\n  }\n\n  inline unsigned mul(unsigned\
    \ a, unsigned b) {\n    return 1ull * a * b % (unsigned long long) mod;\n  }\n\
    \n  void ensure_base(int nbase) {\n    if(nbase <= base) return;\n    rev.resize(1\
    \ << nbase);\n    rts.resize(1 << nbase);\n    for(int i = 0; i < (1 << nbase);\
    \ i++) {\n      rev[i] = (rev[i >> 1] >> 1) + ((i & 1) << (nbase - 1));\n    }\n\
    \    assert(nbase <= max_base);\n    while(base < nbase) {\n      int z = mod_pow(root,\
    \ 1 << (max_base - 1 - base));\n      for(int i = 1 << (base - 1); i < (1 << base);\
    \ i++) {\n        rts[i << 1] = rts[i];\n        rts[(i << 1) + 1] = mul(rts[i],\
    \ z);\n      }\n      ++base;\n    }\n  }\n\n  void ntt(vector< int > &a) {\n\
    \    const int n = (int) a.size();\n    assert((n & (n - 1)) == 0);\n    int zeros\
    \ = __builtin_ctz(n);\n    ensure_base(zeros);\n    int shift = base - zeros;\n\
    \    for(int i = 0; i < n; i++) {\n      if(i < (rev[i] >> shift)) {\n       \
    \ swap(a[i], a[rev[i] >> shift]);\n      }\n    }\n    for(int k = 1; k < n; k\
    \ <<= 1) {\n      for(int i = 0; i < n; i += 2 * k) {\n        for(int j = 0;\
    \ j < k; j++) {\n          int z = mul(a[i + j + k], rts[j + k]);\n          a[i\
    \ + j + k] = add(a[i + j], mod - z);\n          a[i + j] = add(a[i + j], z);\n\
    \        }\n      }\n    }\n  }\n\n  vector< int > multiply(vector< int > a, vector<\
    \ int > b) {\n    int need = a.size() + b.size() - 1;\n    int nbase = 1;\n  \
    \  while((1 << nbase) < need) nbase++;\n    ensure_base(nbase);\n    int sz =\
    \ 1 << nbase;\n    a.resize(sz, 0);\n    b.resize(sz, 0);\n    ntt(a);\n    ntt(b);\n\
    \    int inv_sz = inverse(sz);\n    for(int i = 0; i < sz; i++) {\n      a[i]\
    \ = mul(a[i], mul(b[i], inv_sz));\n    }\n    reverse(a.begin() + 1, a.end());\n\
    \    ntt(a);\n    a.resize(need);\n    return a;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fft/number-theoretic-transform.cpp
  requiredBy: []
  timestamp: '2020-02-24 19:19:55+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-convolution-mod.test.cpp
documentation_of: math/fft/number-theoretic-transform.cpp
layout: document
redirect_from:
- /library/math/fft/number-theoretic-transform.cpp
- /library/math/fft/number-theoretic-transform.cpp.html
title: math/fft/number-theoretic-transform.cpp
---
