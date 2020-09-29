---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 1 \"test/verify/atcoder-tenka1-2016-final-c.cpp\"\n#define IGNORE\n\
    \nint main() {\n  Trie< 26, 'a' > trie;\n  string S, P[5000];\n  int M, W[5000];\n\
    \n  cin >> S;\n  cin >> M;\n  for(int i = 0; i < M; i++) {\n    cin >> P[i];\n\
    \    trie.add(P[i]);\n  }\n  for(int i = 0; i < M; i++) {\n    cin >> W[i];\n\
    \  }\n  vector< int > dp(S.size() + 1);\n  for(int i = 0; i < S.size(); i++) {\n\
    \    auto update = [&](int idx) {\n      dp[i + P[idx].size()] = max(dp[i + P[idx].size()],\
    \ dp[i] + W[idx]);\n    };\n    trie.query(S, update, i, 0);\n    dp[i + 1] =\
    \ max(dp[i + 1], dp[i]);\n  }\n  cout << dp.back() << endl;\n}\n"
  code: "#define IGNORE\n\nint main() {\n  Trie< 26, 'a' > trie;\n  string S, P[5000];\n\
    \  int M, W[5000];\n\n  cin >> S;\n  cin >> M;\n  for(int i = 0; i < M; i++) {\n\
    \    cin >> P[i];\n    trie.add(P[i]);\n  }\n  for(int i = 0; i < M; i++) {\n\
    \    cin >> W[i];\n  }\n  vector< int > dp(S.size() + 1);\n  for(int i = 0; i\
    \ < S.size(); i++) {\n    auto update = [&](int idx) {\n      dp[i + P[idx].size()]\
    \ = max(dp[i + P[idx].size()], dp[i] + W[idx]);\n    };\n    trie.query(S, update,\
    \ i, 0);\n    dp[i + 1] = max(dp[i + 1], dp[i]);\n  }\n  cout << dp.back() <<\
    \ endl;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/atcoder-tenka1-2016-final-c.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/atcoder-tenka1-2016-final-c.cpp
layout: document
redirect_from:
- /library/test/verify/atcoder-tenka1-2016-final-c.cpp
- /library/test/verify/atcoder-tenka1-2016-final-c.cpp.html
title: test/verify/atcoder-tenka1-2016-final-c.cpp
---
