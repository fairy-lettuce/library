---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    document_title: "Moebius Table(\u30E1\u30D3\u30A6\u30B9\u95A2\u6570\u30C6\u30FC\
      \u30D6\u30EB)"
    links: []
  bundledCode: "#line 1 \"math/number-theory/moebius-mu-table.cpp\"\n/**\n * @brief\
    \ Moebius Table(\u30E1\u30D3\u30A6\u30B9\u95A2\u6570\u30C6\u30FC\u30D6\u30EB)\n\
    \ */\nvector< int > moebius_table(int n) {\n  vector< int > mu(n + 1, 1), p(n\
    \ + 1, 1);\n  for(int i = 2; i <= n; i++) {\n    if(p[i] == 1) {\n      for(int\
    \ j = i; j <= n; j += i) p[j] = i;\n    }\n    if((i / p[i]) % p[i] == 0) mu[i]\
    \ = 0;\n    else mu[i] = -mu[i / p[i]];\n  }\n  return mu;\n}\n"
  code: "/**\n * @brief Moebius Table(\u30E1\u30D3\u30A6\u30B9\u95A2\u6570\u30C6\u30FC\
    \u30D6\u30EB)\n */\nvector< int > moebius_table(int n) {\n  vector< int > mu(n\
    \ + 1, 1), p(n + 1, 1);\n  for(int i = 2; i <= n; i++) {\n    if(p[i] == 1) {\n\
    \      for(int j = i; j <= n; j += i) p[j] = i;\n    }\n    if((i / p[i]) % p[i]\
    \ == 0) mu[i] = 0;\n    else mu[i] = -mu[i / p[i]];\n  }\n  return mu;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/number-theory/moebius-mu-table.cpp
  requiredBy: []
  timestamp: '2021-07-16 02:57:30+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: math/number-theory/moebius-mu-table.cpp
layout: document
redirect_from:
- /library/math/number-theory/moebius-mu-table.cpp
- /library/math/number-theory/moebius-mu-table.cpp.html
title: "Moebius Table(\u30E1\u30D3\u30A6\u30B9\u95A2\u6570\u30C6\u30FC\u30D6\u30EB\
  )"
---
