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
  bundledCode: "#line 1 \"test/verify/atcoder-atc-001-c.cpp\"\n#define IGNORE\n\n\
    int main() {\n  int N;\n  scanf(\"%d\", &N);\n  vector< int > A(N + 1), B(N +\
    \ 1);\n  for(int i = 0; i < N; i++) scanf(\"%d %d\", &A[i + 1], &B[i + 1]);\n\
    \  NumberTheoreticTransform< 1012924417 > ntt;\n  auto C = ntt.multiply(A, B);\n\
    \  for(int i = 1; i <= 2 * N; i++) printf(\"%d\\n\", C[i]);\n}\n"
  code: "#define IGNORE\n\nint main() {\n  int N;\n  scanf(\"%d\", &N);\n  vector<\
    \ int > A(N + 1), B(N + 1);\n  for(int i = 0; i < N; i++) scanf(\"%d %d\", &A[i\
    \ + 1], &B[i + 1]);\n  NumberTheoreticTransform< 1012924417 > ntt;\n  auto C =\
    \ ntt.multiply(A, B);\n  for(int i = 1; i <= 2 * N; i++) printf(\"%d\\n\", C[i]);\n\
    }\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/atcoder-atc-001-c.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/atcoder-atc-001-c.cpp
layout: document
redirect_from:
- /library/test/verify/atcoder-atc-001-c.cpp
- /library/test/verify/atcoder-atc-001-c.cpp.html
title: test/verify/atcoder-atc-001-c.cpp
---
