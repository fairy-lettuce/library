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
  bundledCode: "#line 1 \"string/z-algorithm.cpp\"\nvector< int > z_algorithm(const\
    \ string &s) {\n  vector< int > prefix(s.size());\n  for(int i = 1, j = 0; i <\
    \ s.size(); i++) {\n    if(i + prefix[i - j] < j + prefix[j]) {\n      prefix[i]\
    \ = prefix[i - j];\n    } else {\n      int k = max(0, j + prefix[j] - i);\n \
    \     while(i + k < s.size() && s[k] == s[i + k]) ++k;\n      prefix[i] = k;\n\
    \      j = i;\n    }\n  }\n  prefix[0] = (int) s.size();\n  return prefix;\n}\n"
  code: "vector< int > z_algorithm(const string &s) {\n  vector< int > prefix(s.size());\n\
    \  for(int i = 1, j = 0; i < s.size(); i++) {\n    if(i + prefix[i - j] < j +\
    \ prefix[j]) {\n      prefix[i] = prefix[i - j];\n    } else {\n      int k =\
    \ max(0, j + prefix[j] - i);\n      while(i + k < s.size() && s[k] == s[i + k])\
    \ ++k;\n      prefix[i] = k;\n      j = i;\n    }\n  }\n  prefix[0] = (int) s.size();\n\
    \  return prefix;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: string/z-algorithm.cpp
  requiredBy: []
  timestamp: '2019-07-20 01:29:30+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: string/z-algorithm.cpp
layout: document
redirect_from:
- /library/string/z-algorithm.cpp
- /library/string/z-algorithm.cpp.html
title: string/z-algorithm.cpp
---
