---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 1 \"test/verify/spoj-dquery.cpp\"\n#define IGNORE\n\nnt main()\
    \ {\n  int N, Q;\n  cin >> N;\n  vector< int > A(N);\n  for(int i = 0; i < N;\
    \ i++) {\n    cin >> A[i];\n  }\n  cin >> Q;\n  vector< int > f(1000001);\n  Mo\
    \ mo(N, Q);\n  for(int i = 0; i < Q; i++) {\n    int l, r;\n    cin >> l >> r;\n\
    \    mo.add(--l, r);\n  }\n  int ret = 0;\n  auto add = [&](int idx) { if(f[A[idx]]++\
    \ == 0) ret++; };\n  auto del = [&](int idx) { if(f[A[idx]]-- == 1) --ret; };\n\
    \  vector< int > ans(Q);\n  auto rem = [&](int idx) { ans[idx] = ret; };\n  mo.run(add,\
    \ del, rem);\n  for(int i = 0; i < Q; i++) {\n    cout << ans[i] << \"\\n\";\n\
    \  }\n}\n"
  code: "#define IGNORE\n\nnt main() {\n  int N, Q;\n  cin >> N;\n  vector< int >\
    \ A(N);\n  for(int i = 0; i < N; i++) {\n    cin >> A[i];\n  }\n  cin >> Q;\n\
    \  vector< int > f(1000001);\n  Mo mo(N, Q);\n  for(int i = 0; i < Q; i++) {\n\
    \    int l, r;\n    cin >> l >> r;\n    mo.add(--l, r);\n  }\n  int ret = 0;\n\
    \  auto add = [&](int idx) { if(f[A[idx]]++ == 0) ret++; };\n  auto del = [&](int\
    \ idx) { if(f[A[idx]]-- == 1) --ret; };\n  vector< int > ans(Q);\n  auto rem =\
    \ [&](int idx) { ans[idx] = ret; };\n  mo.run(add, del, rem);\n  for(int i = 0;\
    \ i < Q; i++) {\n    cout << ans[i] << \"\\n\";\n  }\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/spoj-dquery.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/spoj-dquery.cpp
layout: document
redirect_from:
- /library/test/verify/spoj-dquery.cpp
- /library/test/verify/spoj-dquery.cpp.html
title: test/verify/spoj-dquery.cpp
---
