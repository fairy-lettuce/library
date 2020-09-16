---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    links: []
  bundledCode: "#line 1 \"string/manacher.cpp\"\nvector< int > manacher(const string\
    \ &s) {\n  vector< int > radius(s.size());\n  int i = 0, j = 0;\n  while(i < s.size())\
    \ {\n    while(i - j >= 0 && i + j < s.size() && s[i - j] == s[i + j]) {\n   \
    \   ++j;\n    }\n    radius[i] = j;\n    int k = 1;\n    while(i - k >= 0 && i\
    \ + k < s.size() && k + radius[i - k] < j) {\n      radius[i + k] = radius[i -\
    \ k];\n      ++k;\n    }\n    i += k;\n    j -= k;\n  }\n  return radius;\n}\n"
  code: "vector< int > manacher(const string &s) {\n  vector< int > radius(s.size());\n\
    \  int i = 0, j = 0;\n  while(i < s.size()) {\n    while(i - j >= 0 && i + j <\
    \ s.size() && s[i - j] == s[i + j]) {\n      ++j;\n    }\n    radius[i] = j;\n\
    \    int k = 1;\n    while(i - k >= 0 && i + k < s.size() && k + radius[i - k]\
    \ < j) {\n      radius[i + k] = radius[i - k];\n      ++k;\n    }\n    i += k;\n\
    \    j -= k;\n  }\n  return radius;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: string/manacher.cpp
  requiredBy: []
  timestamp: '2019-07-20 01:29:30+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: string/manacher.cpp
layout: document
redirect_from:
- /library/string/manacher.cpp
- /library/string/manacher.cpp.html
title: string/manacher.cpp
---
