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
  bundledCode: "#line 1 \"test/verify/codeforces-250-e.cpp\"\n#define IGNORE\n\nint\
    \ main() {\n  int N, M;\n  cin >> N >> M;\n  PolynominalMod< modint > C(M + 1);\n\
    \  C[0] = 1;\n  for(int i = 0; i < N; i++) {\n    int k;\n    cin >> k;\n    if(k\
    \ <= M) C[k] = mod - 4;\n  }\n  C = C.sqrt();\n  C[0] += 1;\n  C = C.inverse();\n\
    \  for(int i = 1; i <= M; i++) {\n    cout << C[i] * 2 << \"\\n\";\n  }\n}\n"
  code: "#define IGNORE\n\nint main() {\n  int N, M;\n  cin >> N >> M;\n  PolynominalMod<\
    \ modint > C(M + 1);\n  C[0] = 1;\n  for(int i = 0; i < N; i++) {\n    int k;\n\
    \    cin >> k;\n    if(k <= M) C[k] = mod - 4;\n  }\n  C = C.sqrt();\n  C[0] +=\
    \ 1;\n  C = C.inverse();\n  for(int i = 1; i <= M; i++) {\n    cout << C[i] *\
    \ 2 << \"\\n\";\n  }\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/codeforces-250-e.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/codeforces-250-e.cpp
layout: document
redirect_from:
- /library/test/verify/codeforces-250-e.cpp
- /library/test/verify/codeforces-250-e.cpp.html
title: test/verify/codeforces-250-e.cpp
---
