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
  bundledCode: "#line 1 \"test/verify/atcoder-shpc-2018-final-e.cpp\"\n#define IGNORE\n\
    \nusing int64 = long long;\n\nint64 power[234567];\nconst int LIM = 1000000;\n\
    \ \nint main() {\n  int N, M;\n  string S[20];\n \n  power[0] = 1;\n  for(int\
    \ i = 0; i < 234566; i++) power[i + 1] = 1LL * power[i] * 1000000 % mod;\n \n\
    \  cin >> N >> M;\n  for(int i = 0; i < M; i++) cin >> S[i];\n  vector< vector<\
    \ pair< int, int > > > dat(M, vector< pair< int, int > >(N));\n  for(int i = 0;\
    \ i < M; i++) {\n    for(int j = 0; j < N; j++) {\n      dat[i][j].first = S[i][j]\
    \ - 'a';\n      dat[i][j].first++;\n      dat[i][j].second = 1;\n    }\n  }\n\
    \  using pi = pair< int, int >;\n  auto F = [&](pi x, pi y) {\n    return pi((1LL\
    \ * y.first * power[x.second] + x.first % mod) % mod, x.second + y.second);\n\
    \  };\n  vector< RandomizedBinarySearchTree< pi > >\n      beet(M, RandomizedBinarySearchTree<\
    \ pi >(N, F, pi(0, 0)));\n  vector< RandomizedBinarySearchTree< pi >::Node * >\
    \ root;\n  for(int i = 0; i < M; i++) root.push_back(beet[i].build(dat[i]));\n\
    \  \n  int Q;\n  cin >> Q;\n  while(Q--) {\n    int T, A, B, C, D;\n    cin >>\
    \ T >> A >> B >> C >> D;\n    --A, --B, --C;\n    if(T == 1) {\n      auto S =\
    \ beet[A].split(root[A], D);\n      auto T = beet[A].split(S.first, C);\n    \
    \  auto U = beet[B].split(root[B], D);\n      auto V = beet[B].split(U.first,\
    \ C);\n      root[A] = beet[A].merge(T.first, beet[A].merge(V.second, S.second));\n\
    \      root[B] = beet[B].merge(V.first, beet[B].merge(T.second, U.second));\n\
    \    } else {\n      auto S = beet[A].split(root[A], D);\n      auto T = beet[A].split(S.first,\
    \ C);\n      printf(\"%d\\n\", beet[A].sum(T.second).first);\n      root[A] =\
    \ beet[A].merge(beet[A].merge(T.first, T.second), S.second);\n    }\n  }\n}\n"
  code: "#define IGNORE\n\nusing int64 = long long;\n\nint64 power[234567];\nconst\
    \ int LIM = 1000000;\n \nint main() {\n  int N, M;\n  string S[20];\n \n  power[0]\
    \ = 1;\n  for(int i = 0; i < 234566; i++) power[i + 1] = 1LL * power[i] * 1000000\
    \ % mod;\n \n  cin >> N >> M;\n  for(int i = 0; i < M; i++) cin >> S[i];\n  vector<\
    \ vector< pair< int, int > > > dat(M, vector< pair< int, int > >(N));\n  for(int\
    \ i = 0; i < M; i++) {\n    for(int j = 0; j < N; j++) {\n      dat[i][j].first\
    \ = S[i][j] - 'a';\n      dat[i][j].first++;\n      dat[i][j].second = 1;\n  \
    \  }\n  }\n  using pi = pair< int, int >;\n  auto F = [&](pi x, pi y) {\n    return\
    \ pi((1LL * y.first * power[x.second] + x.first % mod) % mod, x.second + y.second);\n\
    \  };\n  vector< RandomizedBinarySearchTree< pi > >\n      beet(M, RandomizedBinarySearchTree<\
    \ pi >(N, F, pi(0, 0)));\n  vector< RandomizedBinarySearchTree< pi >::Node * >\
    \ root;\n  for(int i = 0; i < M; i++) root.push_back(beet[i].build(dat[i]));\n\
    \  \n  int Q;\n  cin >> Q;\n  while(Q--) {\n    int T, A, B, C, D;\n    cin >>\
    \ T >> A >> B >> C >> D;\n    --A, --B, --C;\n    if(T == 1) {\n      auto S =\
    \ beet[A].split(root[A], D);\n      auto T = beet[A].split(S.first, C);\n    \
    \  auto U = beet[B].split(root[B], D);\n      auto V = beet[B].split(U.first,\
    \ C);\n      root[A] = beet[A].merge(T.first, beet[A].merge(V.second, S.second));\n\
    \      root[B] = beet[B].merge(V.first, beet[B].merge(T.second, U.second));\n\
    \    } else {\n      auto S = beet[A].split(root[A], D);\n      auto T = beet[A].split(S.first,\
    \ C);\n      printf(\"%d\\n\", beet[A].sum(T.second).first);\n      root[A] =\
    \ beet[A].merge(beet[A].merge(T.first, T.second), S.second);\n    }\n  }\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/atcoder-shpc-2018-final-e.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/atcoder-shpc-2018-final-e.cpp
layout: document
redirect_from:
- /library/test/verify/atcoder-shpc-2018-final-e.cpp
- /library/test/verify/atcoder-shpc-2018-final-e.cpp.html
title: test/verify/atcoder-shpc-2018-final-e.cpp
---
