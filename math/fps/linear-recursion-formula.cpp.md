---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    document_title: Linear-Recursion-Formula
    links: []
  bundledCode: "#line 1 \"math/fps/linear-recursion-formula.cpp\"\n/**\n * @brief\
    \ Linear-Recursion-Formula\n */\ntemplate< template< typename > class FPS, typename\
    \ Mint >\nMint linear_recursion_formula(FPS< Mint > P, FPS< Mint > Q, int64_t\
    \ k) {\n  // compute the coefficient [x^k] P/Q of rational power series\n  Mint\
    \ ret = 0;\n  if(P.size() >= Q.size()) {\n    auto R = P / Q;\n    P -= R * Q;\n\
    \    P.shrink();\n    if(k < (int) R.size()) ret += R[k];\n  }\n  if(P.empty())\
    \ return ret;\n  P.resize((int) Q.size() - 1);\n  auto sub = [&](const FPS< Mint\
    \ > &as, bool odd) {\n    FPS< Mint > bs((as.size() + !odd) / 2);\n    for(int\
    \ i = odd; i < (int) as.size(); i += 2) bs[i >> 1] = as[i];\n    return bs;\n\
    \  };\n  while(k > 0) {\n    auto Q2(Q);\n    for(int i = 1; i < (int) Q2.size();\
    \ i += 2) Q2[i] = -Q2[i];\n    P = sub(P * Q2, k & 1);\n    Q = sub(Q * Q2, 0);\n\
    \    k >>= 1;\n  }\n  return ret + P[0];\n}\n"
  code: "/**\n * @brief Linear-Recursion-Formula\n */\ntemplate< template< typename\
    \ > class FPS, typename Mint >\nMint linear_recursion_formula(FPS< Mint > P, FPS<\
    \ Mint > Q, int64_t k) {\n  // compute the coefficient [x^k] P/Q of rational power\
    \ series\n  Mint ret = 0;\n  if(P.size() >= Q.size()) {\n    auto R = P / Q;\n\
    \    P -= R * Q;\n    P.shrink();\n    if(k < (int) R.size()) ret += R[k];\n \
    \ }\n  if(P.empty()) return ret;\n  P.resize((int) Q.size() - 1);\n  auto sub\
    \ = [&](const FPS< Mint > &as, bool odd) {\n    FPS< Mint > bs((as.size() + !odd)\
    \ / 2);\n    for(int i = odd; i < (int) as.size(); i += 2) bs[i >> 1] = as[i];\n\
    \    return bs;\n  };\n  while(k > 0) {\n    auto Q2(Q);\n    for(int i = 1; i\
    \ < (int) Q2.size(); i += 2) Q2[i] = -Q2[i];\n    P = sub(P * Q2, k & 1);\n  \
    \  Q = sub(Q * Q2, 0);\n    k >>= 1;\n  }\n  return ret + P[0];\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fps/linear-recursion-formula.cpp
  requiredBy: []
  timestamp: '2021-07-13 02:15:10+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: math/fps/linear-recursion-formula.cpp
layout: document
redirect_from:
- /library/math/fps/linear-recursion-formula.cpp
- /library/math/fps/linear-recursion-formula.cpp.html
title: Linear-Recursion-Formula
---
