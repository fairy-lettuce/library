---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 1 \"test/verify/atcoder-cf16-tournament-round3-a.cpp\"\n#define\
    \ IGNORE\n\nint main() {\n  int N, M, K, A[100000];\n  cin >> N >> M >> K;\n \
    \ for(int i = 0; i < N; i++) {\n    cin >> A[i];\n  }\n  vector< int64 > dp(N);\n\
    \  for(int i = 0; i < N; i++) {\n    dp[i] = A[i];\n  }\n  for(int i = 1; i <\
    \ K; i++) {\n    vector< int64 > dp2(N);\n    reverse(begin(dp), end(dp));\n \
    \   dp.resize(N + M - 1);\n    reverse(begin(dp), end(dp));\n    auto p = slide_min(dp,\
    \ M);\n    for(int j = i; j < N; j++) {\n      dp2[j] = max(dp2[j], p[j - 1] +\
    \ 1LL * (i + 1) * A[j]);\n    }\n    dp.swap(dp2);\n  }\n  cout << *max_element(begin(dp),\
    \ end(dp)) << endl;\n}\n\n"
  code: "#define IGNORE\n\nint main() {\n  int N, M, K, A[100000];\n  cin >> N >>\
    \ M >> K;\n  for(int i = 0; i < N; i++) {\n    cin >> A[i];\n  }\n  vector< int64\
    \ > dp(N);\n  for(int i = 0; i < N; i++) {\n    dp[i] = A[i];\n  }\n  for(int\
    \ i = 1; i < K; i++) {\n    vector< int64 > dp2(N);\n    reverse(begin(dp), end(dp));\n\
    \    dp.resize(N + M - 1);\n    reverse(begin(dp), end(dp));\n    auto p = slide_min(dp,\
    \ M);\n    for(int j = i; j < N; j++) {\n      dp2[j] = max(dp2[j], p[j - 1] +\
    \ 1LL * (i + 1) * A[j]);\n    }\n    dp.swap(dp2);\n  }\n  cout << *max_element(begin(dp),\
    \ end(dp)) << endl;\n}\n\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/atcoder-cf16-tournament-round3-a.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/atcoder-cf16-tournament-round3-a.cpp
layout: document
redirect_from:
- /library/test/verify/atcoder-cf16-tournament-round3-a.cpp
- /library/test/verify/atcoder-cf16-tournament-round3-a.cpp.html
title: test/verify/atcoder-cf16-tournament-round3-a.cpp
---
