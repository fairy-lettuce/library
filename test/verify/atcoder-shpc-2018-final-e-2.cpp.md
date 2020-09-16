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
  bundledCode: "#line 1 \"test/verify/atcoder-shpc-2018-final-e-2.cpp\"\n#define IGNORE\n\
    \nusing pi = pair< int, int >;\nusing int64 = long long;\nconst int mod = 1e9\
    \ + 7;\nint64 power[234567];\n \ninline pi none(pi x, int y) { return x; }\n \n\
    inline int none(int x, int y) { return x; }\n \ninline pi F(pi x, pi y) {\n  return\
    \ pi((1LL * y.first * power[x.second] + x.first % mod) % mod, x.second + y.second);\n\
    };\n \n \nint main() {\n  int N, M;\n  string S[20];\n \n  power[0] = 1;\n  for(int\
    \ i = 0; i < 234566; i++) power[i + 1] = 1LL * power[i] * 1000000 % mod;\n \n\
    \  cin >> N >> M;\n  for(int i = 0; i < M; i++) cin >> S[i];\n  vector< vector<\
    \ pair< int, int > > > dat(M, vector< pair< int, int > >(N));\n  for(int i = 0;\
    \ i < M; i++) {\n    for(int j = 0; j < N; j++) {\n      dat[i][j].first = S[i][j]\
    \ - 'a';\n      dat[i][j].first++;\n      dat[i][j].second = 1;\n    }\n  }\n\
    \  using T = RedBlackTree< pi, int, F, none, none, none >;\n  T beet(M * N * 2,\
    \ pi(0, 0), 0);\n  vector< T::Node * > root;\n  for(int i = 0; i < M; i++) root.push_back(beet.build(dat[i]));\n\
    \ \n  int Q;\n  cin >> Q;\n  while(Q--) {\n    int T, A, B, C, D;\n    cin >>\
    \ T >> A >> B >> C >> D;\n    --A, --B, --C;\n    if(T == 1) {\n      auto S =\
    \ beet.split(root[A], D);\n      auto T = beet.split(S.first, C);\n      auto\
    \ U = beet.split(root[B], D);\n      auto V = beet.split(U.first, C);\n      root[A]\
    \ = beet.merge(T.first, beet.merge(V.second, S.second));\n      root[B] = beet.merge(V.first,\
    \ beet.merge(T.second, U.second));\n    } else {\n      auto S = beet.split(root[A],\
    \ D);\n      auto T = beet.split(S.first, C);\n      printf(\"%d\\n\", beet.sum(T.second).first);\n\
    \      root[A] = beet.merge(beet.merge(T.first, T.second), S.second);\n    }\n\
    \  }\n}\n"
  code: "#define IGNORE\n\nusing pi = pair< int, int >;\nusing int64 = long long;\n\
    const int mod = 1e9 + 7;\nint64 power[234567];\n \ninline pi none(pi x, int y)\
    \ { return x; }\n \ninline int none(int x, int y) { return x; }\n \ninline pi\
    \ F(pi x, pi y) {\n  return pi((1LL * y.first * power[x.second] + x.first % mod)\
    \ % mod, x.second + y.second);\n};\n \n \nint main() {\n  int N, M;\n  string\
    \ S[20];\n \n  power[0] = 1;\n  for(int i = 0; i < 234566; i++) power[i + 1] =\
    \ 1LL * power[i] * 1000000 % mod;\n \n  cin >> N >> M;\n  for(int i = 0; i < M;\
    \ i++) cin >> S[i];\n  vector< vector< pair< int, int > > > dat(M, vector< pair<\
    \ int, int > >(N));\n  for(int i = 0; i < M; i++) {\n    for(int j = 0; j < N;\
    \ j++) {\n      dat[i][j].first = S[i][j] - 'a';\n      dat[i][j].first++;\n \
    \     dat[i][j].second = 1;\n    }\n  }\n  using T = RedBlackTree< pi, int, F,\
    \ none, none, none >;\n  T beet(M * N * 2, pi(0, 0), 0);\n  vector< T::Node *\
    \ > root;\n  for(int i = 0; i < M; i++) root.push_back(beet.build(dat[i]));\n\
    \ \n  int Q;\n  cin >> Q;\n  while(Q--) {\n    int T, A, B, C, D;\n    cin >>\
    \ T >> A >> B >> C >> D;\n    --A, --B, --C;\n    if(T == 1) {\n      auto S =\
    \ beet.split(root[A], D);\n      auto T = beet.split(S.first, C);\n      auto\
    \ U = beet.split(root[B], D);\n      auto V = beet.split(U.first, C);\n      root[A]\
    \ = beet.merge(T.first, beet.merge(V.second, S.second));\n      root[B] = beet.merge(V.first,\
    \ beet.merge(T.second, U.second));\n    } else {\n      auto S = beet.split(root[A],\
    \ D);\n      auto T = beet.split(S.first, C);\n      printf(\"%d\\n\", beet.sum(T.second).first);\n\
    \      root[A] = beet.merge(beet.merge(T.first, T.second), S.second);\n    }\n\
    \  }\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/atcoder-shpc-2018-final-e-2.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/atcoder-shpc-2018-final-e-2.cpp
layout: document
redirect_from:
- /library/test/verify/atcoder-shpc-2018-final-e-2.cpp
- /library/test/verify/atcoder-shpc-2018-final-e-2.cpp.html
title: test/verify/atcoder-shpc-2018-final-e-2.cpp
---
