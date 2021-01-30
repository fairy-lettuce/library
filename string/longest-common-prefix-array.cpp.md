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
  bundledCode: "#line 1 \"string/longest-common-prefix-array.cpp\"\nstruct LongestCommonPrefixArray\
    \ {\n  const SuffixArray &SA;\n  vector< int > LCP, rank;\n\n  LongestCommonPrefixArray(const\
    \ SuffixArray &SA) : SA(SA), LCP(SA.size()) {\n    rank.resize(SA.size());\n \
    \   for(int i = 0; i < SA.size(); i++) {\n      rank[SA[i]] = i;\n    }\n    for(int\
    \ i = 0, h = 0; i < SA.size(); i++) {\n      if(rank[i] + 1 < SA.size()) {\n \
    \       for(int j = SA[rank[i] + 1]; max(i, j) + h < SA.size() && SA.s[i + h]\
    \ == SA.s[j + h]; ++h);\n        LCP[rank[i] + 1] = h;\n        if(h > 0) --h;\n\
    \      }\n    }\n  }\n\n  int operator[](int k) const {\n    return LCP[k];\n\
    \  }\n\n  size_t size() const {\n    return LCP.size();\n  }\n\n  void output()\
    \ {\n    for(int i = 0; i < size(); i++) {\n      cout << i << \": \" << LCP[i]\
    \ << \" \" << SA.s.substr(SA[i]) << endl;\n    }\n  }\n};\n"
  code: "struct LongestCommonPrefixArray {\n  const SuffixArray &SA;\n  vector< int\
    \ > LCP, rank;\n\n  LongestCommonPrefixArray(const SuffixArray &SA) : SA(SA),\
    \ LCP(SA.size()) {\n    rank.resize(SA.size());\n    for(int i = 0; i < SA.size();\
    \ i++) {\n      rank[SA[i]] = i;\n    }\n    for(int i = 0, h = 0; i < SA.size();\
    \ i++) {\n      if(rank[i] + 1 < SA.size()) {\n        for(int j = SA[rank[i]\
    \ + 1]; max(i, j) + h < SA.size() && SA.s[i + h] == SA.s[j + h]; ++h);\n     \
    \   LCP[rank[i] + 1] = h;\n        if(h > 0) --h;\n      }\n    }\n  }\n\n  int\
    \ operator[](int k) const {\n    return LCP[k];\n  }\n\n  size_t size() const\
    \ {\n    return LCP.size();\n  }\n\n  void output() {\n    for(int i = 0; i <\
    \ size(); i++) {\n      cout << i << \": \" << LCP[i] << \" \" << SA.s.substr(SA[i])\
    \ << endl;\n    }\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: string/longest-common-prefix-array.cpp
  requiredBy: []
  timestamp: '2019-07-20 01:29:30+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: string/longest-common-prefix-array.cpp
layout: document
redirect_from:
- /library/string/longest-common-prefix-array.cpp
- /library/string/longest-common-prefix-array.cpp.html
title: string/longest-common-prefix-array.cpp
---
