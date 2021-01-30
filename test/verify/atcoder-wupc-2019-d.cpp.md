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
  bundledCode: "#line 1 \"test/verify/atcoder-wupc-2019-d.cpp\"\n#define IGNORE\n\n\
    int main() {\n  int N, M;\n  vector< int > g[100000];\n  cin >> N >> M;\n  for(int\
    \ i = 0; i < M; i++) {\n    int a, b;\n    cin >> a >> b;\n    --a, --b;\n   \
    \ g[b].emplace_back(a);\n  }\n  for(int i = 0; i < N; i++) {\n    g[i].emplace_back(i);\n\
    \  }\n  int in[100000] = {};\n  int ok = 0;\n  SqrtDecomposition< int > tap(N,\
    \ 1);\n  for(int i = 0; i < N; i++) tap.set(i, 1);\n  int ptr = 0, ret = inf,\
    \ l;\n  for(int i = 0; i < N; i++) {\n    while(ptr < N && tap.query_low(0, N)\
    \ < N) {\n      tap.add(0, N);\n      for(auto &to : g[ptr]) tap.sub(to, to +\
    \ 1);\n      ++ptr;\n    }\n    if(tap.query_low(0, N) == N) {\n      if(ptr -\
    \ i < ret) {\n        ret = ptr - i;\n        l = i;\n      }\n    }\n    tap.sub(0,\
    \ N);\n    for(auto &to : g[i]) tap.add(to, to + 1);\n  }\n  if(ret == inf) cout\
    \ << -1 << endl;\n  else cout << l + 1 << \" \" << l + 1 + ret - 1 << endl;\n\
    }\n"
  code: "#define IGNORE\n\nint main() {\n  int N, M;\n  vector< int > g[100000];\n\
    \  cin >> N >> M;\n  for(int i = 0; i < M; i++) {\n    int a, b;\n    cin >> a\
    \ >> b;\n    --a, --b;\n    g[b].emplace_back(a);\n  }\n  for(int i = 0; i < N;\
    \ i++) {\n    g[i].emplace_back(i);\n  }\n  int in[100000] = {};\n  int ok = 0;\n\
    \  SqrtDecomposition< int > tap(N, 1);\n  for(int i = 0; i < N; i++) tap.set(i,\
    \ 1);\n  int ptr = 0, ret = inf, l;\n  for(int i = 0; i < N; i++) {\n    while(ptr\
    \ < N && tap.query_low(0, N) < N) {\n      tap.add(0, N);\n      for(auto &to\
    \ : g[ptr]) tap.sub(to, to + 1);\n      ++ptr;\n    }\n    if(tap.query_low(0,\
    \ N) == N) {\n      if(ptr - i < ret) {\n        ret = ptr - i;\n        l = i;\n\
    \      }\n    }\n    tap.sub(0, N);\n    for(auto &to : g[i]) tap.add(to, to +\
    \ 1);\n  }\n  if(ret == inf) cout << -1 << endl;\n  else cout << l + 1 << \" \"\
    \ << l + 1 + ret - 1 << endl;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/atcoder-wupc-2019-d.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/atcoder-wupc-2019-d.cpp
layout: document
redirect_from:
- /library/test/verify/atcoder-wupc-2019-d.cpp
- /library/test/verify/atcoder-wupc-2019-d.cpp.html
title: test/verify/atcoder-wupc-2019-d.cpp
---
