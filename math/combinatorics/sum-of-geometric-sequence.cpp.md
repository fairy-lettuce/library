---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    document_title: "Sum of Geometric Sequence(\u7B49\u6BD4\u6570\u5217\u306E\u548C\
      )"
    links: []
  bundledCode: "#line 1 \"math/combinatorics/sum-of-geometric-sequence.cpp\"\n/**\n\
    \ * @brief Sum of Geometric Sequence(\u7B49\u6BD4\u6570\u5217\u306E\u548C)\n */\n\
    template< typename Mint >\nMint sum_of_geometric_sequence(const Mint &a, const\
    \ Mint &r, const int64_t &n) {\n  assert(r != Mint(0));\n  return r == Mint(1)\
    \ ? a * n : a * (r.pow(n) - 1) / (r - 1);\n}\n"
  code: "/**\n * @brief Sum of Geometric Sequence(\u7B49\u6BD4\u6570\u5217\u306E\u548C\
    )\n */\ntemplate< typename Mint >\nMint sum_of_geometric_sequence(const Mint &a,\
    \ const Mint &r, const int64_t &n) {\n  assert(r != Mint(0));\n  return r == Mint(1)\
    \ ? a * n : a * (r.pow(n) - 1) / (r - 1);\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/combinatorics/sum-of-geometric-sequence.cpp
  requiredBy: []
  timestamp: '2021-08-09 21:02:39+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: math/combinatorics/sum-of-geometric-sequence.cpp
layout: document
redirect_from:
- /library/math/combinatorics/sum-of-geometric-sequence.cpp
- /library/math/combinatorics/sum-of-geometric-sequence.cpp.html
title: "Sum of Geometric Sequence(\u7B49\u6BD4\u6570\u5217\u306E\u548C)"
---
