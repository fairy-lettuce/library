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
    _deprecated_at_docs: docs/kth-term-of-linearly-recurrent-sequence.md
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
    \ Kth Term of Linearly Recurrent Sequence\n * @docs docs/kth-term-of-linearly-recurrent-sequence.md\n\
    \ */\ntemplate< template< typename > class FPS, typename Mint >\nMint kth_term_of_linearly_recurrent_sequence(const\
    \ FPS< Mint > &a, FPS< Mint > c, int64_t k) {\n  assert(a.size() == c.size());\n\
    \  c = FPS< Mint >{1} - (c << 1);\n  return coeff_of_rational_function((a * c).pre(a.size()),\
    \ c, k);\n}\n"
  code: "#include \"coeff-of-rational-function.cpp\"\n\n/**\n * @brief Kth Term of\
    \ Linearly Recurrent Sequence\n * @docs docs/kth-term-of-linearly-recurrent-sequence.md\n\
    \ */\ntemplate< template< typename > class FPS, typename Mint >\nMint kth_term_of_linearly_recurrent_sequence(const\
    \ FPS< Mint > &a, FPS< Mint > c, int64_t k) {\n  assert(a.size() == c.size());\n\
    \  c = FPS< Mint >{1} - (c << 1);\n  return coeff_of_rational_function((a * c).pre(a.size()),\
    \ c, k);\n}\n"
  dependsOn:
  - math/fps/coeff-of-rational-function.cpp
  isVerificationFile: false
  path: math/fps/kth-term-of-linearly-recurrent-sequence.cpp
  requiredBy: []
  timestamp: '2021-07-14 20:23:23+09:00'
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
## 概要

線形線形漸化的数列の第 $N$ 項を求める。

$k$ 項間漸化式 $a_n = \sum_{d=1}^{k} c_d a_{n-d} (n \ge d)$ が存在するとき数列 $a$ は線形漸化的数列であるという。線形漸化的数列 $a$ は、初項 $(a_1, \cdots, a_{d-1})$ と係数 $c = (c_1, \cdots, c_d), c_d \neq 0$ を用いることで定義される。$d$ を位数と呼ぶ。

位数 $d$ の線形漸化式が存在するとき、ある次数 $d$ の $Q(0)=1$ 満たす多項式 $Q(x)$ と次数 $d-1$ 以下の多項式 $P(x)$ が存在して、$G(x)=\frac {P(x)} {Q(x)}$ が母関数となる。具体的には、

$Q(x) = 1 - c_1x - c_2x^2 - \cdots - c_kx^k$

$P(x) = Q(x)(a_0 + a_1x + a_2x^2 + \cdots + a^{k-1}x^{k-1}) \pmod {x^k}$

とすればよい。$P(x)$ は $Q(x)$ と $a$ を畳み込むと求められる。

従って、数列 $a$ の第 $N$ 項を求めるために、 $\frac {P(x)} {Q(x)}$ の $x^N$ の係数を求めればよくて、Bostan-Mori Algorithm を用いることで効率的に計算できる。


## 計算量

$O(K \log K \log N)$
