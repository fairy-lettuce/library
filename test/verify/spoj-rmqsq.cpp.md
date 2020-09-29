---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 1 \"test/verify/spoj-rmqsq.cpp\"\n#define IGNORE\n\nint main()\
    \ {\n  int N, Q;\n  scanf(\"%d\", &N);\n  vector< int > vs(N);\n  for(int i =\
    \ 0; i < N; i++) scanf(\"%d\", &vs[i]);\n  SparseTable< int > table(vs);\n  scanf(\"\
    %d\", &Q);\n  while(Q--) {\n    int x, y;\n    scanf(\"%d %d\", &x, &y);\n   \
    \ printf(\"%d\\n\", table.rmq(x, y + 1));\n  }\n}\n"
  code: "#define IGNORE\n\nint main() {\n  int N, Q;\n  scanf(\"%d\", &N);\n  vector<\
    \ int > vs(N);\n  for(int i = 0; i < N; i++) scanf(\"%d\", &vs[i]);\n  SparseTable<\
    \ int > table(vs);\n  scanf(\"%d\", &Q);\n  while(Q--) {\n    int x, y;\n    scanf(\"\
    %d %d\", &x, &y);\n    printf(\"%d\\n\", table.rmq(x, y + 1));\n  }\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/spoj-rmqsq.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/spoj-rmqsq.cpp
layout: document
redirect_from:
- /library/test/verify/spoj-rmqsq.cpp
- /library/test/verify/spoj-rmqsq.cpp.html
title: test/verify/spoj-rmqsq.cpp
---
