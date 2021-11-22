---
data:
  _extendedDependsOn: []
  _extendedRequiredBy:
  - icon: ':heavy_check_mark:'
    path: math/fps/multipoint-evaluation.cpp
    title: Multipoint Evaluation
  - icon: ':heavy_check_mark:'
    path: math/fps/polynomial-interpolation.cpp
    title: "Polynomial Interpolation(\u591A\u9805\u5F0F\u88DC\u9593)"
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-multipoint-evaluation.test.cpp
    title: test/verify/yosupo-multipoint-evaluation.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-polynomial-interpolation.test.cpp
    title: test/verify/yosupo-polynomial-interpolation.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    document_title: Subproduct Tree
    links: []
  bundledCode: "#line 1 \"math/fps/subproduct-tree.cpp\"\n/**\n * @brief Subproduct\
    \ Tree\n */\ntemplate< template< typename > class FPS, typename Mint >\nvector<\
    \ FPS< Mint > > subproduct_tree(const FPS< Mint > &xs) {\n  int n = (int) xs.size();\n\
    \  int k = 1;\n  while(k < n) k <<= 1;\n  vector< FPS< Mint > > g(2 * k, {1});\n\
    \  for(int i = 0; i < n; i++) g[k + i] = {-xs[i], Mint(1)};\n  for(int i = k;\
    \ i-- > 1;) g[i] = g[i << 1] * g[i << 1 | 1];\n  return g;\n}\n"
  code: "/**\n * @brief Subproduct Tree\n */\ntemplate< template< typename > class\
    \ FPS, typename Mint >\nvector< FPS< Mint > > subproduct_tree(const FPS< Mint\
    \ > &xs) {\n  int n = (int) xs.size();\n  int k = 1;\n  while(k < n) k <<= 1;\n\
    \  vector< FPS< Mint > > g(2 * k, {1});\n  for(int i = 0; i < n; i++) g[k + i]\
    \ = {-xs[i], Mint(1)};\n  for(int i = k; i-- > 1;) g[i] = g[i << 1] * g[i << 1\
    \ | 1];\n  return g;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fps/subproduct-tree.cpp
  requiredBy:
  - math/fps/multipoint-evaluation.cpp
  - math/fps/polynomial-interpolation.cpp
  timestamp: '2021-07-13 20:24:08+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-polynomial-interpolation.test.cpp
  - test/verify/yosupo-multipoint-evaluation.test.cpp
documentation_of: math/fps/subproduct-tree.cpp
layout: document
redirect_from:
- /library/math/fps/subproduct-tree.cpp
- /library/math/fps/subproduct-tree.cpp.html
title: Subproduct Tree
---
