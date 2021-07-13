---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: math/fps/coeff-of-rational-function.cpp
    title: Coeff of Rational Function
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-kth-term-of-linearly-recurrent-sequence.test.cpp
    title: test/verify/yosupo-kth-term-of-linearly-recurrent-sequence.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    document_title: Kth Term of Linearly Recurrent Sequence
    links: []
  bundledCode: "#line 1 \"math/fps/coeff-of-rational-function.cpp\"\n/**\n * @brief\
    \ Coeff of Rational Function\n * @docs docs/coeff-of-rational-function.md\n */\n\
    template< template< typename > class FPS, typename Mint >\nMint coeff_of_rational_function(FPS<\
    \ Mint > P, FPS< Mint > Q, int64_t k) {\n  // compute the coefficient [x^k] P/Q\
    \ of rational power series\n  Mint ret = 0;\n  if(P.size() >= Q.size()) {\n  \
    \  auto R = P / Q;\n    P -= R * Q;\n    P.shrink();\n    if(k < (int) R.size())\
    \ ret += R[k];\n  }\n  if(P.empty()) return ret;\n  P.resize((int) Q.size() -\
    \ 1);\n  auto sub = [&](const FPS< Mint > &as, bool odd) {\n    FPS< Mint > bs((as.size()\
    \ + !odd) / 2);\n    for(int i = odd; i < (int) as.size(); i += 2) bs[i >> 1]\
    \ = as[i];\n    return bs;\n  };\n  while(k > 0) {\n    auto Q2(Q);\n    for(int\
    \ i = 1; i < (int) Q2.size(); i += 2) Q2[i] = -Q2[i];\n    P = sub(P * Q2, k &\
    \ 1);\n    Q = sub(Q * Q2, 0);\n    k >>= 1;\n  }\n  return ret + P[0];\n}\n#line\
    \ 2 \"math/fps/kth-term-of-linearly-recurrent-sequence.cpp\"\n\n/**\n * @brief\
    \ Kth Term of Linearly Recurrent Sequence\n */\ntemplate< template< typename >\
    \ class FPS, typename Mint >\nMint kth_term_of_linearly_recurrent_sequence(const\
    \ FPS< Mint > &a, FPS< Mint > c, int64_t k) {\n  assert(a.size() == c.size());\n\
    \  c = FPS< Mint >{1} - (c << 1);\n  return coeff_of_rational_function((a * c).pre(a.size()),\
    \ c, k);\n}\n"
  code: "#include \"coeff-of-rational-function.cpp\"\n\n/**\n * @brief Kth Term of\
    \ Linearly Recurrent Sequence\n */\ntemplate< template< typename > class FPS,\
    \ typename Mint >\nMint kth_term_of_linearly_recurrent_sequence(const FPS< Mint\
    \ > &a, FPS< Mint > c, int64_t k) {\n  assert(a.size() == c.size());\n  c = FPS<\
    \ Mint >{1} - (c << 1);\n  return coeff_of_rational_function((a * c).pre(a.size()),\
    \ c, k);\n}\n"
  dependsOn:
  - math/fps/coeff-of-rational-function.cpp
  isVerificationFile: false
  path: math/fps/kth-term-of-linearly-recurrent-sequence.cpp
  requiredBy: []
  timestamp: '2021-07-13 20:24:08+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-kth-term-of-linearly-recurrent-sequence.test.cpp
documentation_of: math/fps/kth-term-of-linearly-recurrent-sequence.cpp
layout: document
redirect_from:
- /library/math/fps/kth-term-of-linearly-recurrent-sequence.cpp
- /library/math/fps/kth-term-of-linearly-recurrent-sequence.cpp.html
title: Kth Term of Linearly Recurrent Sequence
---
