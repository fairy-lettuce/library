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
  bundledCode: "#line 1 \"other/random-number-generator.cpp\"\nstruct RandomNumberGenerator\
    \ {\n  mt19937 mt;\n\n  RandomNumberGenerator() : mt(chrono::steady_clock::now().time_since_epoch().count())\
    \ {}\n\n  int operator()(int a, int b) { // [a, b)\n    uniform_int_distribution<\
    \ int > dist(a, b - 1);\n    return dist(mt);\n  }\n\n  int operator()(int b)\
    \ { // [0, b)\n    return (*this)(0, b);\n  }\n};\n"
  code: "struct RandomNumberGenerator {\n  mt19937 mt;\n\n  RandomNumberGenerator()\
    \ : mt(chrono::steady_clock::now().time_since_epoch().count()) {}\n\n  int operator()(int\
    \ a, int b) { // [a, b)\n    uniform_int_distribution< int > dist(a, b - 1);\n\
    \    return dist(mt);\n  }\n\n  int operator()(int b) { // [0, b)\n    return\
    \ (*this)(0, b);\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: other/random-number-generator.cpp
  requiredBy: []
  timestamp: '2019-07-20 01:29:30+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: other/random-number-generator.cpp
layout: document
redirect_from:
- /library/other/random-number-generator.cpp
- /library/other/random-number-generator.cpp.html
title: other/random-number-generator.cpp
---
