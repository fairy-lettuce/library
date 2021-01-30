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
  bundledCode: "#line 1 \"test/verify/atcoder-arc-030-d.cpp\"\n#define IGNORE\n\n\
    using int64 = long long;\n \nint64 add(int64 x, int64 y) { return x + y; }\n \n\
    int64 mul(int64 x, int y) { return x * y; }\n \nint main() {\n  int N, Q;\n  scanf(\"\
    %d %d\", &N, &Q);\n  vector< int64 > x(N);\n  for(int i = 0; i < N; i++) {\n \
    \   scanf(\"%lld\", &x[i]);\n  }\n  const int LIM = 10000000;\n  PersistentRedBlackTree<\
    \ int64, int64, add, add, add, mul > beet(LIM, 0, 0);\n  auto root = beet.build(x);\n\
    \  int a, b, c, d;\n \n  while(Q--) {\n    scanf(\"%d\", &a);\n    if(a == 1)\
    \ {\n      scanf(\"%d %d %d\", &a, &b, &c);\n      beet.set_propagate(root, --a,\
    \ b, c);\n    } else if(a == 2) {\n      scanf(\"%d %d %d %d\", &a, &b, &c, &d);\n\
    \      auto S = beet.split(root, b);\n      auto T = beet.split(S.first, --a);\n\
    \      auto U = beet.split(root, d);\n      auto V = beet.split(U.first, --c);\n\
    \      root = beet.merge(T.first, beet.merge(V.second, S.second));\n    } else\
    \ {\n      scanf(\"%d %d\", &a, &b);\n      auto S = beet.split(root, b);\n  \
    \    auto T = beet.split(S.first, --a);\n      printf(\"%lld\\n\", beet.sum(T.second));\n\
    \    }\n    if(beet.pool.ptr < 1000) root = beet.rebuild(root);\n  }\n}\n"
  code: "#define IGNORE\n\nusing int64 = long long;\n \nint64 add(int64 x, int64 y)\
    \ { return x + y; }\n \nint64 mul(int64 x, int y) { return x * y; }\n \nint main()\
    \ {\n  int N, Q;\n  scanf(\"%d %d\", &N, &Q);\n  vector< int64 > x(N);\n  for(int\
    \ i = 0; i < N; i++) {\n    scanf(\"%lld\", &x[i]);\n  }\n  const int LIM = 10000000;\n\
    \  PersistentRedBlackTree< int64, int64, add, add, add, mul > beet(LIM, 0, 0);\n\
    \  auto root = beet.build(x);\n  int a, b, c, d;\n \n  while(Q--) {\n    scanf(\"\
    %d\", &a);\n    if(a == 1) {\n      scanf(\"%d %d %d\", &a, &b, &c);\n      beet.set_propagate(root,\
    \ --a, b, c);\n    } else if(a == 2) {\n      scanf(\"%d %d %d %d\", &a, &b, &c,\
    \ &d);\n      auto S = beet.split(root, b);\n      auto T = beet.split(S.first,\
    \ --a);\n      auto U = beet.split(root, d);\n      auto V = beet.split(U.first,\
    \ --c);\n      root = beet.merge(T.first, beet.merge(V.second, S.second));\n \
    \   } else {\n      scanf(\"%d %d\", &a, &b);\n      auto S = beet.split(root,\
    \ b);\n      auto T = beet.split(S.first, --a);\n      printf(\"%lld\\n\", beet.sum(T.second));\n\
    \    }\n    if(beet.pool.ptr < 1000) root = beet.rebuild(root);\n  }\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/atcoder-arc-030-d.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/atcoder-arc-030-d.cpp
layout: document
redirect_from:
- /library/test/verify/atcoder-arc-030-d.cpp
- /library/test/verify/atcoder-arc-030-d.cpp.html
title: test/verify/atcoder-arc-030-d.cpp
---
