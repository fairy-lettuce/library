---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    _deprecated_at_docs: docs/divisor.md
    document_title: "Divisor(\u7D04\u6570\u5217\u6319)"
    links: []
  bundledCode: "#line 1 \"math/number-theory/divisor.cpp\"\n/**\n * @brief Divisor(\u7D04\
    \u6570\u5217\u6319)\n * @docs docs/divisor.md\n */\nvector< int64_t > divisor(int64_t\
    \ n) {\n  vector< int64_t > ret;\n  for(int64_t i = 1; i * i <= n; i++) {\n  \
    \  if(n % i == 0) {\n      ret.push_back(i);\n      if(i * i != n) ret.push_back(n\
    \ / i);\n    }\n  }\n  sort(begin(ret), end(ret));\n  return ret;\n}\n"
  code: "/**\n * @brief Divisor(\u7D04\u6570\u5217\u6319)\n * @docs docs/divisor.md\n\
    \ */\nvector< int64_t > divisor(int64_t n) {\n  vector< int64_t > ret;\n  for(int64_t\
    \ i = 1; i * i <= n; i++) {\n    if(n % i == 0) {\n      ret.push_back(i);\n \
    \     if(i * i != n) ret.push_back(n / i);\n    }\n  }\n  sort(begin(ret), end(ret));\n\
    \  return ret;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/number-theory/divisor.cpp
  requiredBy: []
  timestamp: '2020-02-24 19:08:02+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: math/number-theory/divisor.cpp
layout: document
redirect_from:
- /library/math/number-theory/divisor.cpp
- /library/math/number-theory/divisor.cpp.html
title: "Divisor(\u7D04\u6570\u5217\u6319)"
---
## 概要

ある数の約数を列挙する.

* `divisor(n)`: `n` の約数を返す.

## 計算量

* $O(\sqrt n)$
