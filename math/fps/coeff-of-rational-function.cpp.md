---
data:
  _extendedDependsOn: []
  _extendedRequiredBy:
  - icon: ':heavy_check_mark:'
    path: math/fps/kth-term-of-linearly-recurrent-sequence.cpp
    title: Kth-Term-Of-Linearly-Recurrent-Sequence
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-kth-term-of-linearly-recurrent-sequence.test.cpp
    title: test/verify/yosupo-kth-term-of-linearly-recurrent-sequence.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/coeff-of-rational-function.md
    document_title: Coeff of Rational Function
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
    \ 1);\n    Q = sub(Q * Q2, 0);\n    k >>= 1;\n  }\n  return ret + P[0];\n}\n"
  code: "/**\n * @brief Coeff of Rational Function\n * @docs docs/coeff-of-rational-function.md\n\
    \ */\ntemplate< template< typename > class FPS, typename Mint >\nMint coeff_of_rational_function(FPS<\
    \ Mint > P, FPS< Mint > Q, int64_t k) {\n  // compute the coefficient [x^k] P/Q\
    \ of rational power series\n  Mint ret = 0;\n  if(P.size() >= Q.size()) {\n  \
    \  auto R = P / Q;\n    P -= R * Q;\n    P.shrink();\n    if(k < (int) R.size())\
    \ ret += R[k];\n  }\n  if(P.empty()) return ret;\n  P.resize((int) Q.size() -\
    \ 1);\n  auto sub = [&](const FPS< Mint > &as, bool odd) {\n    FPS< Mint > bs((as.size()\
    \ + !odd) / 2);\n    for(int i = odd; i < (int) as.size(); i += 2) bs[i >> 1]\
    \ = as[i];\n    return bs;\n  };\n  while(k > 0) {\n    auto Q2(Q);\n    for(int\
    \ i = 1; i < (int) Q2.size(); i += 2) Q2[i] = -Q2[i];\n    P = sub(P * Q2, k &\
    \ 1);\n    Q = sub(Q * Q2, 0);\n    k >>= 1;\n  }\n  return ret + P[0];\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fps/coeff-of-rational-function.cpp
  requiredBy:
  - math/fps/kth-term-of-linearly-recurrent-sequence.cpp
  timestamp: '2021-07-13 19:38:41+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-kth-term-of-linearly-recurrent-sequence.test.cpp
documentation_of: math/fps/coeff-of-rational-function.cpp
layout: document
redirect_from:
- /library/math/fps/coeff-of-rational-function.cpp
- /library/math/fps/coeff-of-rational-function.cpp.html
title: Coeff of Rational Function
---
## 概要

$K$ 次多項式 $P(x), Q(x)$ に対して $\displaystyle [x^N] \frac{P(x)}{Q(x)}$ を Bostan-Mori algorithm によって計算する。

## 線形漸化的数列の第 $N$ 項

このアルゴリズムを用いることで、線形線形漸化的数列の第 $N$ 項を同じ計算量で求めることが出来る。

$k$ 項間漸化式 $a_n = \sum_{d=1}^{k} c_d a_{n-d} (n \ge d)$ が存在するとき数列 $a$ は線形漸化的数列であるという。線形漸化的数列 $a$ は、初項 $(a_1, \cdots, a_{d-1})$ と係数 $c = (c_1, \cdots, c_d), c_d \neq 0$ を用いることで定義される。$d$ を位数と呼ぶ。

位数 $d$ の線形漸化式が存在するとき、ある次数 $d$ の $Q(0)=1$ 満たす多項式 $Q(x)$ と次数 $d-1$ 以下の多項式 $P(x)$ が存在して、$G(x)=\frac {P(x)} {Q(x)}$ が母関数となる。具体的には、

$Q(x) = 1 - c_1x - c_2x^2 - \cdots - c_kx^k$

$P(x) = Q(x)(a_0 + a_1x + a_2x^2 + \cdots + a^{k-1}x^{k-1}) \pmod {x^k}$

とすればよい。$P(x)$ は $Q(x)$ と $a$ を畳み込むと求められる。

従って、数列 $a$ の第 $N$ 項を求めるために、 $\frac {P(x)} {Q(x)}$ の $x^N$ の係数を求めればよくて、Bostan-Mori Algorithm を用いることで効率的に計算できる。

## 計算量

$O(K \log K \log N)$
