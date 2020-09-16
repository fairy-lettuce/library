---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    IGNORE: ''
    IGNORE_IF_CLANG: ''
    IGNORE_IF_GCC: ''
    links: []
  bundledCode: "#line 1 \"test/verify/atcoder-colopl2018-final-c.cpp\"\n#define IGNORE\n\
    \nint main() {\n  int N;\n  cin >> N;\n  vector< int64_t > A(N);\n  for(auto &p\
    \ : A) cin >> p;\n  function< int64_t(int, int) > f = [&](int i, int j) { return\
    \ A[j] + 1LL * (j - i) * (j - i); };\n  for(auto &p : monotone_minima(N, N, f))\
    \ cout << p.second << endl;\n}\n\n"
  code: "#define IGNORE\n\nint main() {\n  int N;\n  cin >> N;\n  vector< int64_t\
    \ > A(N);\n  for(auto &p : A) cin >> p;\n  function< int64_t(int, int) > f = [&](int\
    \ i, int j) { return A[j] + 1LL * (j - i) * (j - i); };\n  for(auto &p : monotone_minima(N,\
    \ N, f)) cout << p.second << endl;\n}\n\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/atcoder-colopl2018-final-c.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/atcoder-colopl2018-final-c.cpp
layout: document
redirect_from:
- /library/test/verify/atcoder-colopl2018-final-c.cpp
- /library/test/verify/atcoder-colopl2018-final-c.cpp.html
title: test/verify/atcoder-colopl2018-final-c.cpp
---
