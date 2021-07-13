---
data:
  _extendedDependsOn:
  - icon: ':question:'
    path: math/combinatorics/enumeration.cpp
    title: math/combinatorics/enumeration.cpp
  - icon: ':x:'
    path: math/combinatorics/sample-point-shift.cpp
    title: Sample-Point-Shift
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':x:'
    path: test/verify/yukicoder-502.test.cpp
    title: test/verify/yukicoder-502.test.cpp
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes:
    document_title: "Factorial(\u968E\u4E57)"
    links: []
  bundledCode: "#line 1 \"math/combinatorics/enumeration.cpp\"\ntemplate< typename\
    \ T >\nstruct Enumeration {\nprivate:\n  static vector< T > _fact, _finv, _inv;\n\
    \n  inline static void expand(size_t sz) {\n    if(_fact.size() < sz + 1) {\n\
    \      int pre_sz = max(1, (int) _fact.size());\n      _fact.resize(sz + 1, T(1));\n\
    \      _finv.resize(sz + 1, T(1));\n      _inv.resize(sz + 1, T(1));\n      for(int\
    \ i = pre_sz; i <= (int) sz; i++) {\n        _fact[i] = _fact[i - 1] * T(i);\n\
    \      }\n      _finv[sz] = T(1) / _fact[sz];\n      for(int i = (int) sz - 1;\
    \ i >= pre_sz; i--) {\n        _finv[i] = _finv[i + 1] * T(i + 1);\n      }\n\
    \      for(int i = pre_sz; i <= (int) sz; i++) {\n        _inv[i] = _finv[i] *\
    \ _fact[i - 1];\n      }\n    }\n  }\n\npublic:\n  explicit Enumeration(size_t\
    \ sz = 0) { expand(sz); }\n\n  static inline T fact(int k) {\n    expand(k);\n\
    \    return _fact[k];\n  }\n\n  static inline T finv(int k) {\n    expand(k);\n\
    \    return _finv[k];\n  }\n\n  static inline T inv(int k) {\n    expand(k);\n\
    \    return _inv[k];\n  }\n\n  static T P(int n, int r) {\n    if(r < 0 || n <\
    \ r) return 0;\n    return fact(n) * finv(n - r);\n  }\n\n  static T C(int p,\
    \ int q) {\n    if(q < 0 || p < q) return 0;\n    return fact(p) * finv(q) * finv(p\
    \ - q);\n  }\n\n  static T H(int n, int r) {\n    if(n < 0 || r < 0) return 0;\n\
    \    return r == 0 ? 1 : C(n + r - 1, r);\n  }\n};\n\ntemplate< typename T >\n\
    vector< T > Enumeration< T >::_fact = vector< T >();\ntemplate< typename T >\n\
    vector< T > Enumeration< T >::_finv = vector< T >();\ntemplate< typename T >\n\
    vector< T > Enumeration< T >::_inv = vector< T >();\n#line 2 \"math/combinatorics/sample-point-shift.cpp\"\
    \n\n/**\n * @brief Sample-Point-Shift\n */\ntemplate< typename Mint, typename\
    \ F >\nvector< Mint > sample_point_shift(const vector< Mint > &ys, const Mint\
    \ &m, const F &multiply) {\n  Enumeration< Mint > comb;\n  int d = (int) ys.size()\
    \ - 1;\n  vector< Mint > f(d + 1), g(d * 2 + 1);\n  for(int i = 0; i <= d; i++)\
    \ {\n    f[i] = ys[i] * comb.finv(i) * comb.finv(d - i);\n    if((d - i) & 1)\
    \ f[i] = -f[i];\n  }\n  for(int i = 0; i <= 2 * d; i++) {\n    g[i] = Mint(1)\
    \ / (m - d + i);\n  }\n  auto h = multiply(f, g);\n  Mint coef = 1;\n  for(int\
    \ i = 0; i <= d; i++) {\n    coef *= (m - d + i);\n  }\n  for(int i = 0; i <=\
    \ d; i++) {\n    h[i + d] *= coef;\n    coef *= (m + i + 1) * g[i];\n  }\n  return\
    \ vector< Mint >{begin(h) + d, begin(h) + 2 * d + 1};\n}\n#line 2 \"math/combinatorics/factorial.cpp\"\
    \n\n/**\n * @brief Factorial(\u968E\u4E57)\n */\ntemplate< typename Mint, typename\
    \ F >\nMint factorial(int64_t n, const F& multiply) {\n  if(n <= 1) return 1;\n\
    \  if(n >= Mint::get_mod()) return 0;\n  int64_t v = 1;\n  while(v * v < n) v\
    \ *= 2;\n  Mint iv = Mint(1) / v;\n  vector< Mint > G{1, v + 1};\n  for(int64_t\
    \ d = 1; d != v; d <<= 1) {\n    vector< Mint > G1 = sample_point_shift(G, Mint(d)\
    \ * iv, multiply);\n    vector< Mint > G2 = sample_point_shift(G, Mint(d * v +\
    \ v) * iv, multiply);\n    vector< Mint > G3 = sample_point_shift(G, Mint(d *\
    \ v + d + v) * iv, multiply);\n    for(int i = 0; i <= d; i++) G[i] *= G1[i],\
    \ G2[i] *= G3[i];\n    copy(begin(G2), end(G2) - 1, back_inserter(G));\n  }\n\
    \  Mint res = 1;\n  int64_t i = 0;\n  while(i + v <= n) res *= G[i / v], i +=\
    \ v;\n  while(i < n) res *= ++i;\n  return res;\n}\n"
  code: "#include \"sample-point-shift.cpp\"\n\n/**\n * @brief Factorial(\u968E\u4E57\
    )\n */\ntemplate< typename Mint, typename F >\nMint factorial(int64_t n, const\
    \ F& multiply) {\n  if(n <= 1) return 1;\n  if(n >= Mint::get_mod()) return 0;\n\
    \  int64_t v = 1;\n  while(v * v < n) v *= 2;\n  Mint iv = Mint(1) / v;\n  vector<\
    \ Mint > G{1, v + 1};\n  for(int64_t d = 1; d != v; d <<= 1) {\n    vector< Mint\
    \ > G1 = sample_point_shift(G, Mint(d) * iv, multiply);\n    vector< Mint > G2\
    \ = sample_point_shift(G, Mint(d * v + v) * iv, multiply);\n    vector< Mint >\
    \ G3 = sample_point_shift(G, Mint(d * v + d + v) * iv, multiply);\n    for(int\
    \ i = 0; i <= d; i++) G[i] *= G1[i], G2[i] *= G3[i];\n    copy(begin(G2), end(G2)\
    \ - 1, back_inserter(G));\n  }\n  Mint res = 1;\n  int64_t i = 0;\n  while(i +\
    \ v <= n) res *= G[i / v], i += v;\n  while(i < n) res *= ++i;\n  return res;\n\
    }\n"
  dependsOn:
  - math/combinatorics/sample-point-shift.cpp
  - math/combinatorics/enumeration.cpp
  isVerificationFile: false
  path: math/combinatorics/factorial.cpp
  requiredBy: []
  timestamp: '2021-06-29 02:11:11+09:00'
  verificationStatus: LIBRARY_ALL_WA
  verifiedWith:
  - test/verify/yukicoder-502.test.cpp
documentation_of: math/combinatorics/factorial.cpp
layout: document
redirect_from:
- /library/math/combinatorics/factorial.cpp
- /library/math/combinatorics/factorial.cpp.html
title: "Factorial(\u968E\u4E57)"
---
