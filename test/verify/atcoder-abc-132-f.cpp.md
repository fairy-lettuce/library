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
  bundledCode: "#line 1 \"test/verify/atcoder-abc-132-f.cpp\"\n#define IGNORE\n\n\
    int main() {\n  int N, K;\n  cin >> N >> K;\n  auto range = quotient_range(N);\n\
    \n  vector< modint > dp(range.size());\n  dp[0] = 1;\n  for(int i = 0; i < K;\
    \ i++) {\n    reverse(begin(dp), end(dp));\n    vector< modint > dp2(range.size());\n\
    \    modint add = 0;\n    for(int j = range.size() - 1; j >= 0; j--) {\n     \
    \ add += dp[j];\n      dp2[j] = add * (range[j].first.second - range[j].first.first\
    \ + 1);\n    }\n    dp.swap(dp2);\n  }\n  modint ret;\n  for(auto &t : dp) ret\
    \ += t;\n  cout << ret << endl;\n}\n\n"
  code: "#define IGNORE\n\nint main() {\n  int N, K;\n  cin >> N >> K;\n  auto range\
    \ = quotient_range(N);\n\n  vector< modint > dp(range.size());\n  dp[0] = 1;\n\
    \  for(int i = 0; i < K; i++) {\n    reverse(begin(dp), end(dp));\n    vector<\
    \ modint > dp2(range.size());\n    modint add = 0;\n    for(int j = range.size()\
    \ - 1; j >= 0; j--) {\n      add += dp[j];\n      dp2[j] = add * (range[j].first.second\
    \ - range[j].first.first + 1);\n    }\n    dp.swap(dp2);\n  }\n  modint ret;\n\
    \  for(auto &t : dp) ret += t;\n  cout << ret << endl;\n}\n\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/atcoder-abc-132-f.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/atcoder-abc-132-f.cpp
layout: document
redirect_from:
- /library/test/verify/atcoder-abc-132-f.cpp
- /library/test/verify/atcoder-abc-132-f.cpp.html
title: test/verify/atcoder-abc-132-f.cpp
---
