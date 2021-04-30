---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-grl-1-a-3.test.cpp
    title: test/verify/aoj-grl-1-a-3.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links: []
  bundledCode: "#line 1 \"structure/heap/radix-heap.cpp\"\ntemplate< typename key_t,\
    \ typename val_t >\nstruct RadixHeap {\n  static constexpr int bit = sizeof(key_t)\
    \ * 8;\n  array< vector< pair< key_t, val_t > >, bit > vs;\n\n  size_t sz;\n \
    \ key_t last;\n\n  RadixHeap() : sz(0), last(0) {}\n\n  bool empty() const { return\
    \ sz == 0; }\n\n  size_t size() const { return sz; }\n\n  inline int getbit(int\
    \ a) const {\n    return a ? bit - __builtin_clz(a) : 0;\n  }\n\n  inline int\
    \ getbit(int64_t a) const {\n    return a ? bit - __builtin_clzll(a) : 0;\n  }\n\
    \n  void push(const key_t &key, const val_t &val) {\n    sz++;\n    vs[getbit(key\
    \ ^ last)].emplace_back(key, val);\n  }\n\n  pair< key_t, val_t > pop() {\n  \
    \  if(vs[0].empty()) {\n      int idx = 1;\n      while(vs[idx].empty()) idx++;\n\
    \      last = min_element(vs[idx].begin(), vs[idx].end())->first;\n      for(auto\
    \ &p:vs[idx]) vs[getbit(p.first ^ last)].emplace_back(p);\n      vs[idx].clear();\n\
    \    }\n    --sz;\n    auto res = vs[0].back();\n    vs[0].pop_back();\n    return\
    \ res;\n  }\n};\n"
  code: "template< typename key_t, typename val_t >\nstruct RadixHeap {\n  static\
    \ constexpr int bit = sizeof(key_t) * 8;\n  array< vector< pair< key_t, val_t\
    \ > >, bit > vs;\n\n  size_t sz;\n  key_t last;\n\n  RadixHeap() : sz(0), last(0)\
    \ {}\n\n  bool empty() const { return sz == 0; }\n\n  size_t size() const { return\
    \ sz; }\n\n  inline int getbit(int a) const {\n    return a ? bit - __builtin_clz(a)\
    \ : 0;\n  }\n\n  inline int getbit(int64_t a) const {\n    return a ? bit - __builtin_clzll(a)\
    \ : 0;\n  }\n\n  void push(const key_t &key, const val_t &val) {\n    sz++;\n\
    \    vs[getbit(key ^ last)].emplace_back(key, val);\n  }\n\n  pair< key_t, val_t\
    \ > pop() {\n    if(vs[0].empty()) {\n      int idx = 1;\n      while(vs[idx].empty())\
    \ idx++;\n      last = min_element(vs[idx].begin(), vs[idx].end())->first;\n \
    \     for(auto &p:vs[idx]) vs[getbit(p.first ^ last)].emplace_back(p);\n     \
    \ vs[idx].clear();\n    }\n    --sz;\n    auto res = vs[0].back();\n    vs[0].pop_back();\n\
    \    return res;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/heap/radix-heap.cpp
  requiredBy: []
  timestamp: '2019-11-30 22:41:48+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-grl-1-a-3.test.cpp
documentation_of: structure/heap/radix-heap.cpp
layout: document
redirect_from:
- /library/structure/heap/radix-heap.cpp
- /library/structure/heap/radix-heap.cpp.html
title: structure/heap/radix-heap.cpp
---
