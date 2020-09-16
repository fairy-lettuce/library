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
  bundledCode: "#line 1 \"other/mo-rollback.cpp\"\nstruct MoRollBack {\n  using ADD\
    \ = function< void(int) >;\n  using REM = function< void(int) >;\n  using RESET\
    \ = function< void() >;\n  using SNAPSHOT = function< void() >;\n  using ROLLBACK\
    \ = function< void() >;\n\n  int width;\n  vector< int > left, right, order;\n\
    \n  MoRollBack(int N, int Q) : width((int) sqrt(N)), order(Q) {\n    iota(begin(order),\
    \ end(order), 0);\n  }\n\n  void add(int l, int r) { /* [l, r) */\n    left.emplace_back(l);\n\
    \    right.emplace_back(r);\n  }\n\n  int run(const ADD &add, const REM &rem,\
    \ const RESET &reset, const SNAPSHOT &snapshot, const ROLLBACK &rollback) {\n\
    \    assert(left.size() == order.size());\n    sort(begin(order), end(order),\
    \ [&](int a, int b) {\n      int ablock = left[a] / width, bblock = left[b] /\
    \ width;\n      if(ablock != bblock) return ablock < bblock;\n      return right[a]\
    \ < right[b];\n    });\n    reset();\n    for(auto idx : order) {\n      if(right[idx]\
    \ - left[idx] < width) {\n        for(int i = left[idx]; i < right[idx]; i++)\
    \ add(i);\n        rem(idx);\n        rollback();\n      }\n    }\n    int nr\
    \ = 0, last_block = -1;\n    for(auto idx : order) {\n      if(right[idx] - left[idx]\
    \ < width) continue;\n      int block = left[idx] / width;\n      if(last_block\
    \ != block) {\n        reset();\n        last_block = block;\n        nr = (block\
    \ + 1) * width;\n      }\n      while(nr < right[idx]) add(nr++);\n      snapshot();\n\
    \      for(int j = (block + 1) * width - 1; j >= left[idx]; j--) add(j);\n   \
    \   rem(idx);\n      rollback();\n    }\n  }\n};\n\n"
  code: "struct MoRollBack {\n  using ADD = function< void(int) >;\n  using REM =\
    \ function< void(int) >;\n  using RESET = function< void() >;\n  using SNAPSHOT\
    \ = function< void() >;\n  using ROLLBACK = function< void() >;\n\n  int width;\n\
    \  vector< int > left, right, order;\n\n  MoRollBack(int N, int Q) : width((int)\
    \ sqrt(N)), order(Q) {\n    iota(begin(order), end(order), 0);\n  }\n\n  void\
    \ add(int l, int r) { /* [l, r) */\n    left.emplace_back(l);\n    right.emplace_back(r);\n\
    \  }\n\n  int run(const ADD &add, const REM &rem, const RESET &reset, const SNAPSHOT\
    \ &snapshot, const ROLLBACK &rollback) {\n    assert(left.size() == order.size());\n\
    \    sort(begin(order), end(order), [&](int a, int b) {\n      int ablock = left[a]\
    \ / width, bblock = left[b] / width;\n      if(ablock != bblock) return ablock\
    \ < bblock;\n      return right[a] < right[b];\n    });\n    reset();\n    for(auto\
    \ idx : order) {\n      if(right[idx] - left[idx] < width) {\n        for(int\
    \ i = left[idx]; i < right[idx]; i++) add(i);\n        rem(idx);\n        rollback();\n\
    \      }\n    }\n    int nr = 0, last_block = -1;\n    for(auto idx : order) {\n\
    \      if(right[idx] - left[idx] < width) continue;\n      int block = left[idx]\
    \ / width;\n      if(last_block != block) {\n        reset();\n        last_block\
    \ = block;\n        nr = (block + 1) * width;\n      }\n      while(nr < right[idx])\
    \ add(nr++);\n      snapshot();\n      for(int j = (block + 1) * width - 1; j\
    \ >= left[idx]; j--) add(j);\n      rem(idx);\n      rollback();\n    }\n  }\n\
    };\n\n"
  dependsOn: []
  isVerificationFile: false
  path: other/mo-rollback.cpp
  requiredBy: []
  timestamp: '2019-07-20 01:29:30+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: other/mo-rollback.cpp
layout: document
redirect_from:
- /library/other/mo-rollback.cpp
- /library/other/mo-rollback.cpp.html
title: other/mo-rollback.cpp
---
