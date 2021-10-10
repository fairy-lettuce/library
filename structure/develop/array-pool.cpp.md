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
  bundledCode: "#line 1 \"structure/develop/array-pool.cpp\"\ntemplate< class T, size_t\
    \ V >\nstruct ArrayPool {\n  array< T, V > pool;\n  array< T *, V > stock;\n \
    \ int ptr;\n\n  ArrayPool() { clear(); }\n\n  inline T *alloc() {\n    return\
    \ stock[--ptr];\n  }\n\n  inline void free(T *t) {\n    stock[ptr++] = t;\n  }\n\
    \n  void clear() {\n    ptr = (int) pool.size();\n    for(int i = 0; i < pool.size();\
    \ i++) stock[i] = &pool[i];\n  }\n};\n"
  code: "template< class T, size_t V >\nstruct ArrayPool {\n  array< T, V > pool;\n\
    \  array< T *, V > stock;\n  int ptr;\n\n  ArrayPool() { clear(); }\n\n  inline\
    \ T *alloc() {\n    return stock[--ptr];\n  }\n\n  inline void free(T *t) {\n\
    \    stock[ptr++] = t;\n  }\n\n  void clear() {\n    ptr = (int) pool.size();\n\
    \    for(int i = 0; i < pool.size(); i++) stock[i] = &pool[i];\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/develop/array-pool.cpp
  requiredBy: []
  timestamp: '2020-11-04 13:55:57+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: structure/develop/array-pool.cpp
layout: document
redirect_from:
- /library/structure/develop/array-pool.cpp
- /library/structure/develop/array-pool.cpp.html
title: structure/develop/array-pool.cpp
---
