---
data:
  _extendedDependsOn:
  - icon: ':warning:'
    path: math/fps/sample-point-shift.cpp
    title: Sample-Point-Shift
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    document_title: "Factorial(\u968E\u4E57)"
    links: []
  bundledCode: "#line 1 \"math/fps/sample-point-shift.cpp\"\n/**\n * @brief Sample-Point-Shift\n\
    \ */\ntemplate< template< typename > class FPS, typename Mint >\nFPS< Mint > sample_point_shift(const\
    \ FPS< Mint > &ys, const Mint &m) {\n  Enumeration< Mint > comb;\n  int d = (int)\
    \ ys.size() - 1;\n  FPS< Mint > f(d + 1), g(d * 2 + 1);\n  for(int i = 0; i <=\
    \ d; i++) {\n    f[i] = ys[i] * comb.finv(i) * comb.finv(d - i);\n    if((d -\
    \ i) & 1) f[i] = -f[i];\n  }\n  for(int i = 0; i <= 2 * d; i++) {\n    g[i] =\
    \ modint(1) / (m - d + i);\n  }\n  auto h = f * g;\n  Mint coef = 1;\n  for(int\
    \ i = 0; i <= d; i++) {\n    coef *= (m - d + i);\n  }\n  for(int i = 0; i <=\
    \ d; i++) {\n    h[i + d] *= coef;\n    coef *= (m + i + 1) * g[i];\n  }\n  return\
    \ FPS< Mint >{begin(h) + d, begin(h) + 2 * d + 1};\n}\n#line 2 \"math/fps/factorial.cpp\"\
    \n\n/**\n * @brief Factorial(\u968E\u4E57)\n */\ntemplate< template< typename\
    \ > class FPS, typename Mint >\nMint factorial(int n) {\n  if(n <= 1) return 1;\n\
    \  if(n >= Mint::get_mod()) return 0;\n  long long v = 1;\n  while(v * v < n)\
    \ v *= 2;\n  Mint iv = Mint(1) / v;\n  FPS< Mint > G{1, v + 1};\n  for(long long\
    \ d = 1; d != v; d <<= 1) {\n    FPS< Mint > G1 = sample_point_shift(G, Mint(d)\
    \ * iv);\n    FPS< Mint > G2 = sample_point_shift(G, Mint(d * v + v) * iv);\n\
    \    FPS< Mint > G3 = sample_point_shift(G, Mint(d * v + d + v) * iv);\n    for(int\
    \ i = 0; i <= d; i++) G[i] *= G1[i], G2[i] *= G3[i];\n    copy(begin(G2), end(G2)\
    \ - 1, back_inserter(G));\n  }\n  Mint res = 1;\n  long long i = 0;\n  while(i\
    \ + v <= n) res *= G[i / v], i += v;\n  while(i < n) res *= ++i;\n  return res;\n\
    }\n"
  code: "#include \"sample-point-shift.cpp\"\n\n/**\n * @brief Factorial(\u968E\u4E57\
    )\n */\ntemplate< template< typename > class FPS, typename Mint >\nMint factorial(int\
    \ n) {\n  if(n <= 1) return 1;\n  if(n >= Mint::get_mod()) return 0;\n  long long\
    \ v = 1;\n  while(v * v < n) v *= 2;\n  Mint iv = Mint(1) / v;\n  FPS< Mint >\
    \ G{1, v + 1};\n  for(long long d = 1; d != v; d <<= 1) {\n    FPS< Mint > G1\
    \ = sample_point_shift(G, Mint(d) * iv);\n    FPS< Mint > G2 = sample_point_shift(G,\
    \ Mint(d * v + v) * iv);\n    FPS< Mint > G3 = sample_point_shift(G, Mint(d *\
    \ v + d + v) * iv);\n    for(int i = 0; i <= d; i++) G[i] *= G1[i], G2[i] *= G3[i];\n\
    \    copy(begin(G2), end(G2) - 1, back_inserter(G));\n  }\n  Mint res = 1;\n \
    \ long long i = 0;\n  while(i + v <= n) res *= G[i / v], i += v;\n  while(i <\
    \ n) res *= ++i;\n  return res;\n}\n"
  dependsOn:
  - math/fps/sample-point-shift.cpp
  isVerificationFile: false
  path: math/fps/factorial.cpp
  requiredBy: []
  timestamp: '2021-06-29 01:28:49+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: math/fps/factorial.cpp
layout: document
redirect_from:
- /library/math/fps/factorial.cpp
- /library/math/fps/factorial.cpp.html
title: "Factorial(\u968E\u4E57)"
---
