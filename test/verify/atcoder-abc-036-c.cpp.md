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
  bundledCode: "#line 1 \"test/verify/atcoder-abc-036-c.cpp\"\n#define IGNORE\n\n\
    int main() {\n  int N;\n  cin >> N;\n  vector< int64 > A(N);\n  cin >> A;\n  Compress<\
    \ int64 > comp(A);\n  comp.build();\n  for(auto &p : comp.get(A)) cout << p <<\
    \ \"\\n\";\n}\n"
  code: "#define IGNORE\n\nint main() {\n  int N;\n  cin >> N;\n  vector< int64 >\
    \ A(N);\n  cin >> A;\n  Compress< int64 > comp(A);\n  comp.build();\n  for(auto\
    \ &p : comp.get(A)) cout << p << \"\\n\";\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/atcoder-abc-036-c.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/atcoder-abc-036-c.cpp
layout: document
redirect_from:
- /library/test/verify/atcoder-abc-036-c.cpp
- /library/test/verify/atcoder-abc-036-c.cpp.html
title: test/verify/atcoder-abc-036-c.cpp
---
