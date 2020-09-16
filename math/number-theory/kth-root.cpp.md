---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-kth-root-integer.test.cpp
    title: test/verify/yosupo-kth-root-integer.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    document_title: Kth-Root
    links: []
  bundledCode: "#line 1 \"math/number-theory/kth-root.cpp\"\n/**\n * @brief Kth-Root\n\
    \ */\nuint64_t kth_root(uint64_t a, int k) {\n  if(k == 1) return a;\n  auto check\
    \ = [&](uint32_t x) {\n    uint64_t mul = 1;\n    for(int j = 0; j < k; j++) {\n\
    \      if(__builtin_mul_overflow(mul, x, &mul)) return false;\n    }\n    return\
    \ mul <= a;\n  };\n  uint64_t ret = 0;\n  for(int i = 31; i >= 0; i--) {\n   \
    \ if(check(ret | (1u << i))) ret |= 1u << i;\n  }\n  return ret;\n}\n"
  code: "/**\n * @brief Kth-Root\n */\nuint64_t kth_root(uint64_t a, int k) {\n  if(k\
    \ == 1) return a;\n  auto check = [&](uint32_t x) {\n    uint64_t mul = 1;\n \
    \   for(int j = 0; j < k; j++) {\n      if(__builtin_mul_overflow(mul, x, &mul))\
    \ return false;\n    }\n    return mul <= a;\n  };\n  uint64_t ret = 0;\n  for(int\
    \ i = 31; i >= 0; i--) {\n    if(check(ret | (1u << i))) ret |= 1u << i;\n  }\n\
    \  return ret;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/number-theory/kth-root.cpp
  requiredBy: []
  timestamp: '2020-03-03 18:40:18+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-kth-root-integer.test.cpp
documentation_of: math/number-theory/kth-root.cpp
layout: document
redirect_from:
- /library/math/number-theory/kth-root.cpp
- /library/math/number-theory/kth-root.cpp.html
title: Kth-Root
---
