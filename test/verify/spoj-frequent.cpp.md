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
  bundledCode: "#line 1 \"test/verify/spoj-frequent.cpp\"\n#define IGNORE\n\nint main()\
    \ {\n  int N, Q;\n  while(cin >> N, N) {\n    cin >> Q;\n    vector< int > A(N);\n\
    \    for(int i = 0; i < N; i++) {\n      cin >> A[i];\n      A[i] += 100000;\n\
    \    }\n    vector< int > f(200001), g(200001);\n    Mo mo(N, Q);\n    for(int\
    \ i = 0; i < Q; i++) {\n      int l, r;\n      cin >> l >> r;\n      mo.add(--l,\
    \ r);\n    }\n    int ret = 0;\n    auto add = [&](int idx) {\n      g[f[A[idx]]]--;\n\
    \      f[A[idx]]++;\n      g[f[A[idx]]]++;\n      if(f[A[idx]] > ret) ++ret;\n\
    \    };\n    auto del = [&](int idx) {\n      g[f[A[idx]]]--;\n      f[A[idx]]--;\n\
    \      g[f[A[idx]]]++;\n      if(ret - 1 == f[A[idx]] && g[ret] == 0) --ret;\n\
    \    };\n    vector< int > ans(Q);\n    auto rem = [&](int idx) { ans[idx] = ret;\
    \ };\n    mo.run(add, del, rem);\n    for(int i = 0; i < Q; i++) {\n      cout\
    \ << ans[i] << \"\\n\";\n    }\n  }\n}\n"
  code: "#define IGNORE\n\nint main() {\n  int N, Q;\n  while(cin >> N, N) {\n   \
    \ cin >> Q;\n    vector< int > A(N);\n    for(int i = 0; i < N; i++) {\n     \
    \ cin >> A[i];\n      A[i] += 100000;\n    }\n    vector< int > f(200001), g(200001);\n\
    \    Mo mo(N, Q);\n    for(int i = 0; i < Q; i++) {\n      int l, r;\n      cin\
    \ >> l >> r;\n      mo.add(--l, r);\n    }\n    int ret = 0;\n    auto add = [&](int\
    \ idx) {\n      g[f[A[idx]]]--;\n      f[A[idx]]++;\n      g[f[A[idx]]]++;\n \
    \     if(f[A[idx]] > ret) ++ret;\n    };\n    auto del = [&](int idx) {\n    \
    \  g[f[A[idx]]]--;\n      f[A[idx]]--;\n      g[f[A[idx]]]++;\n      if(ret -\
    \ 1 == f[A[idx]] && g[ret] == 0) --ret;\n    };\n    vector< int > ans(Q);\n \
    \   auto rem = [&](int idx) { ans[idx] = ret; };\n    mo.run(add, del, rem);\n\
    \    for(int i = 0; i < Q; i++) {\n      cout << ans[i] << \"\\n\";\n    }\n \
    \ }\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/spoj-frequent.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/spoj-frequent.cpp
layout: document
redirect_from:
- /library/test/verify/spoj-frequent.cpp
- /library/test/verify/spoj-frequent.cpp.html
title: test/verify/spoj-frequent.cpp
---
