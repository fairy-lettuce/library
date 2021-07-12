---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-multipoint-evaluation.test.cpp
    title: test/verify/yosupo-multipoint-evaluation.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    document_title: Multipoint-Evaluation
    links: []
  bundledCode: "#line 1 \"math/fps/multipoint-evaluation.cpp\"\n/**\n * @brief Multipoint-Evaluation\n\
    \ */\ntemplate< template< typename > class FPS, typename Mint >\nFPS< Mint > multipoint_evaluation(const\
    \ FPS< Mint > &f, const FPS< Mint > &xs) {\n  int n = (int) f.size(), m = (int)\
    \ xs.size();\n  int k = 1;\n  while(k < m) k <<= 1;\n  vector< FPS< Mint > > g(2\
    \ * k, {1});\n  for(int i = 0; i < m; i++) g[k + i] = {-xs[i], Mint(1)};\n  for(int\
    \ i = k; i-- > 1;) g[i] = g[i << 1] * g[i << 1 | 1];\n  g[1] = f % g[1];\n  for(int\
    \ i = 2; i < k + m; i++) g[i] = g[i >> 1] % g[i];\n  FPS< Mint > ys(m);\n  for(int\
    \ i = 0; i < m; i++) ys[i] = g[k + i][0];\n  return ys;\n}\n"
  code: "/**\n * @brief Multipoint-Evaluation\n */\ntemplate< template< typename >\
    \ class FPS, typename Mint >\nFPS< Mint > multipoint_evaluation(const FPS< Mint\
    \ > &f, const FPS< Mint > &xs) {\n  int n = (int) f.size(), m = (int) xs.size();\n\
    \  int k = 1;\n  while(k < m) k <<= 1;\n  vector< FPS< Mint > > g(2 * k, {1});\n\
    \  for(int i = 0; i < m; i++) g[k + i] = {-xs[i], Mint(1)};\n  for(int i = k;\
    \ i-- > 1;) g[i] = g[i << 1] * g[i << 1 | 1];\n  g[1] = f % g[1];\n  for(int i\
    \ = 2; i < k + m; i++) g[i] = g[i >> 1] % g[i];\n  FPS< Mint > ys(m);\n  for(int\
    \ i = 0; i < m; i++) ys[i] = g[k + i][0];\n  return ys;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fps/multipoint-evaluation.cpp
  requiredBy: []
  timestamp: '2021-07-12 18:11:22+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-multipoint-evaluation.test.cpp
documentation_of: math/fps/multipoint-evaluation.cpp
layout: document
redirect_from:
- /library/math/fps/multipoint-evaluation.cpp
- /library/math/fps/multipoint-evaluation.cpp.html
title: Multipoint-Evaluation
---
