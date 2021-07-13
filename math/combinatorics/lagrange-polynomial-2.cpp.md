---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    document_title: "Lagrange Polynomial(\u591A\u9805\u5F0F\u88DC\u9593, \u4FC2\u6570\
      )"
    links: []
  bundledCode: "#line 1 \"math/combinatorics/lagrange-polynomial-2.cpp\"\n/**\n *\
    \ @brief Lagrange Polynomial(\u591A\u9805\u5F0F\u88DC\u9593, \u4FC2\u6570)\n */\n\
    template< typename Mint >\nvector< Mint > lagrange_polynomial(const vector< Mint\
    \ > &x, const vector< Mint > &y) {\n  int k = (int) x.size() - 1;\n\n  vector<\
    \ Mint > f(k + 1), dp(k + 2);\n  dp[0] = 1;\n  for(int j = 0; j <= k; j++) {\n\
    \    for(int l = k + 1; l > 0; l--) {\n      dp[l] = dp[l] * -x[j] + dp[l - 1];\n\
    \    }\n    dp[0] *= -x[j];\n  }\n\n  for(int i = 0; i <= k; i++) {\n    Mint\
    \ d = 1;\n    for(int j = 0; j <= k; j++) {\n      if(i != j) {\n        d *=\
    \ x[i] - x[j];\n      }\n    }\n    Mint mul = y[i] / d;\n    if(x[i] == 0) {\n\
    \      for(int j = 0; j <= k; j++) {\n        f[j] += dp[j + 1] * mul;\n     \
    \ }\n    } else {\n      Mint inv = Mint(1) / (-x[i]), pre = 0;\n      for(int\
    \ j = 0; j <= k; j++) {\n        Mint cur = (dp[j] - pre) * inv;\n        f[j]\
    \ += cur * mul;\n        pre = cur;\n      }\n    }\n  }\n  return f;\n}\n"
  code: "/**\n * @brief Lagrange Polynomial(\u591A\u9805\u5F0F\u88DC\u9593, \u4FC2\
    \u6570)\n */\ntemplate< typename Mint >\nvector< Mint > lagrange_polynomial(const\
    \ vector< Mint > &x, const vector< Mint > &y) {\n  int k = (int) x.size() - 1;\n\
    \n  vector< Mint > f(k + 1), dp(k + 2);\n  dp[0] = 1;\n  for(int j = 0; j <= k;\
    \ j++) {\n    for(int l = k + 1; l > 0; l--) {\n      dp[l] = dp[l] * -x[j] +\
    \ dp[l - 1];\n    }\n    dp[0] *= -x[j];\n  }\n\n  for(int i = 0; i <= k; i++)\
    \ {\n    Mint d = 1;\n    for(int j = 0; j <= k; j++) {\n      if(i != j) {\n\
    \        d *= x[i] - x[j];\n      }\n    }\n    Mint mul = y[i] / d;\n    if(x[i]\
    \ == 0) {\n      for(int j = 0; j <= k; j++) {\n        f[j] += dp[j + 1] * mul;\n\
    \      }\n    } else {\n      Mint inv = Mint(1) / (-x[i]), pre = 0;\n      for(int\
    \ j = 0; j <= k; j++) {\n        Mint cur = (dp[j] - pre) * inv;\n        f[j]\
    \ += cur * mul;\n        pre = cur;\n      }\n    }\n  }\n  return f;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/combinatorics/lagrange-polynomial-2.cpp
  requiredBy: []
  timestamp: '2021-07-13 23:55:09+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: math/combinatorics/lagrange-polynomial-2.cpp
layout: document
redirect_from:
- /library/math/combinatorics/lagrange-polynomial-2.cpp
- /library/math/combinatorics/lagrange-polynomial-2.cpp.html
title: "Lagrange Polynomial(\u591A\u9805\u5F0F\u88DC\u9593, \u4FC2\u6570)"
---
