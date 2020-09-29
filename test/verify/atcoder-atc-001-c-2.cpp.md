---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 1 \"test/verify/atcoder-atc-001-c-2.cpp\"\n#define IGNORE\n\n\
    int main() {\n  int N;\n  cin >> N;\n  vector< int > A(N + 1), B(N + 1);\n  for(int\
    \ i = 1; i <= N; i++) cin >> A[i] >> B[i];\n  auto C = FastFourierTransform::multiply(A,\
    \ B);\n  for(int i = 1; i <= 2 * N; i++) cout << C[i] << \"\\n\";\n}\n"
  code: "#define IGNORE\n\nint main() {\n  int N;\n  cin >> N;\n  vector< int > A(N\
    \ + 1), B(N + 1);\n  for(int i = 1; i <= N; i++) cin >> A[i] >> B[i];\n  auto\
    \ C = FastFourierTransform::multiply(A, B);\n  for(int i = 1; i <= 2 * N; i++)\
    \ cout << C[i] << \"\\n\";\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/atcoder-atc-001-c-2.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:41:33+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/atcoder-atc-001-c-2.cpp
layout: document
redirect_from:
- /library/test/verify/atcoder-atc-001-c-2.cpp
- /library/test/verify/atcoder-atc-001-c-2.cpp.html
title: test/verify/atcoder-atc-001-c-2.cpp
---
