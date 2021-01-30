---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 1 \"test/verify/codeforces-438-f.cpp\"\n#define IGNORE\n\nint\
    \ main() {\n  int N, K;\n  cin >> N >> K;\n  vector< int > A(N);\n  for(int i\
    \ = 0; i < N; i++) {\n    cin >> A[i];\n    --A[i];\n  }\n  constexpr int64_t\
    \ INF = 1LL << 58;\n\n  int64 L = 0, R = 0, sum = 0;\n  vector< int > appear(100000);\n\
    \  auto add = [&](int idx) { sum += appear[A[idx]]++; };\n  auto del = [&](int\
    \ idx) { sum -= --appear[A[idx]]; };\n  function< int64_t(int l, int r) > f =\
    \ [&](int l, int r) {\n    while(L > l) add(--L);\n    while(R < r) add(R++);\n\
    \    while(L < l) del(L++);\n    while(R > r) del(--R);\n    return sum;\n  };\n\
    \  cout << divide_and_conquer_optimization(K, N, INF, f).back().back() << endl;\n\
    }\n\n"
  code: "#define IGNORE\n\nint main() {\n  int N, K;\n  cin >> N >> K;\n  vector<\
    \ int > A(N);\n  for(int i = 0; i < N; i++) {\n    cin >> A[i];\n    --A[i];\n\
    \  }\n  constexpr int64_t INF = 1LL << 58;\n\n  int64 L = 0, R = 0, sum = 0;\n\
    \  vector< int > appear(100000);\n  auto add = [&](int idx) { sum += appear[A[idx]]++;\
    \ };\n  auto del = [&](int idx) { sum -= --appear[A[idx]]; };\n  function< int64_t(int\
    \ l, int r) > f = [&](int l, int r) {\n    while(L > l) add(--L);\n    while(R\
    \ < r) add(R++);\n    while(L < l) del(L++);\n    while(R > r) del(--R);\n   \
    \ return sum;\n  };\n  cout << divide_and_conquer_optimization(K, N, INF, f).back().back()\
    \ << endl;\n}\n\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/codeforces-438-f.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/codeforces-438-f.cpp
layout: document
redirect_from:
- /library/test/verify/codeforces-438-f.cpp
- /library/test/verify/codeforces-438-f.cpp.html
title: test/verify/codeforces-438-f.cpp
---
