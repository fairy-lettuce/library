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
  bundledCode: "#line 1 \"test/verify/yukicoder-3046.cpp\"\n#define IGNORE\n\nint\
    \ main() {\n  int K, N;\n  cin >> K >> N;\n  PolynominalMod< modint > X(K + 1);\n\
    \  X[0] = 1;\n  for(int i = 0; i < N; i++) {\n    int x;\n    cin >> x;\n    if(x\
    \ <= K) X[x] = -1;\n  }\n  cout << X.inverse()[K] << endl;\n}\n"
  code: "#define IGNORE\n\nint main() {\n  int K, N;\n  cin >> K >> N;\n  PolynominalMod<\
    \ modint > X(K + 1);\n  X[0] = 1;\n  for(int i = 0; i < N; i++) {\n    int x;\n\
    \    cin >> x;\n    if(x <= K) X[x] = -1;\n  }\n  cout << X.inverse()[K] << endl;\n\
    }\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/yukicoder-3046.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/yukicoder-3046.cpp
layout: document
redirect_from:
- /library/test/verify/yukicoder-3046.cpp
- /library/test/verify/yukicoder-3046.cpp.html
title: test/verify/yukicoder-3046.cpp
---
