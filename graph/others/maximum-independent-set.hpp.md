---
data:
  _extendedDependsOn:
  - icon: ':question:'
    path: graph/template.hpp
    title: graph/template.hpp
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':x:'
    path: test/verify/yosupo-maximum-independent-set.test.cpp
    title: test/verify/yosupo-maximum-independent-set.test.cpp
  _isVerificationFailed: true
  _pathExtension: hpp
  _verificationStatusIcon: ':x:'
  attributes:
    links: []
  bundledCode: "#line 2 \"graph/others/maximum-independent-set.hpp\"\n\n#line 2 \"\
    graph/template.hpp\"\n\ntemplate< typename T >\nstruct edge {\n  int src, to;\n\
    \  T cost;\n\n  edge(int to, T cost) : src(-1), to(to), cost(cost) {}\n\n  edge(int\
    \ src, int to, T cost) : src(src), to(to), cost(cost) {}\n\n  edge &operator=(const\
    \ int &x) {\n    to = x;\n    return *this;\n  }\n\n  operator int() const { return\
    \ to; }\n};\n\ntemplate< typename T >\nusing Edges = vector< edge< T > >;\ntemplate<\
    \ typename T >\nusing WeightedGraph = vector< Edges< T > >;\nusing UnWeightedGraph\
    \ = vector< vector< int > >;\ntemplate< typename T >\nusing Matrix = vector< vector<\
    \ T > >;\n#line 4 \"graph/others/maximum-independent-set.hpp\"\n\ntemplate< typename\
    \ T >\nvector< int > maximum_independent_set(const Matrix< T > &g, int trial =\
    \ 1000000) {\n\n  int N = (int) g.size();\n  vector< uint64_t > bit(N);\n\n  assert(N\
    \ <= 64);\n  for(int i = 0; i < N; i++) {\n    for(int j = 0; j < N; j++) {\n\
    \      if(i != j) {\n        assert(g[i][j] == g[j][i]);\n        if(g[i][j])\
    \ bit[i] |= uint64_t(1) << j;\n      }\n    }\n  }\n\n  vector< int > ord(N);\n\
    \  iota(begin(ord), end(ord), 0);\n  mt19937 mt(chrono::steady_clock::now().time_since_epoch().count());\n\
    \  int ret = 0;\n  uint64_t ver = 0;\n  for(int i = 0; i < trial; i++) {\n   \
    \ shuffle(begin(ord), end(ord), mt);\n    uint64_t used = 0;\n    int add = 0;\n\
    \    for(int j : ord) {\n      if(used & bit[j]) continue;\n      used |= uint64_t(1)\
    \ << j;\n      ++add;\n    }\n    if(ret < add) {\n      ret = add;\n      ver\
    \ = used;\n    }\n  }\n  vector< int > ans;\n  for(int i = 0; i < N; i++) {\n\
    \    if((ver >> i) & 1) ans.emplace_back(i);\n  }\n  return ans;\n}\n"
  code: "#pragma once\n\n#include \"../../graph/template.hpp\"\n\ntemplate< typename\
    \ T >\nvector< int > maximum_independent_set(const Matrix< T > &g, int trial =\
    \ 1000000) {\n\n  int N = (int) g.size();\n  vector< uint64_t > bit(N);\n\n  assert(N\
    \ <= 64);\n  for(int i = 0; i < N; i++) {\n    for(int j = 0; j < N; j++) {\n\
    \      if(i != j) {\n        assert(g[i][j] == g[j][i]);\n        if(g[i][j])\
    \ bit[i] |= uint64_t(1) << j;\n      }\n    }\n  }\n\n  vector< int > ord(N);\n\
    \  iota(begin(ord), end(ord), 0);\n  mt19937 mt(chrono::steady_clock::now().time_since_epoch().count());\n\
    \  int ret = 0;\n  uint64_t ver = 0;\n  for(int i = 0; i < trial; i++) {\n   \
    \ shuffle(begin(ord), end(ord), mt);\n    uint64_t used = 0;\n    int add = 0;\n\
    \    for(int j : ord) {\n      if(used & bit[j]) continue;\n      used |= uint64_t(1)\
    \ << j;\n      ++add;\n    }\n    if(ret < add) {\n      ret = add;\n      ver\
    \ = used;\n    }\n  }\n  vector< int > ans;\n  for(int i = 0; i < N; i++) {\n\
    \    if((ver >> i) & 1) ans.emplace_back(i);\n  }\n  return ans;\n}\n"
  dependsOn:
  - graph/template.hpp
  isVerificationFile: false
  path: graph/others/maximum-independent-set.hpp
  requiredBy: []
  timestamp: '2021-07-01 02:53:34+09:00'
  verificationStatus: LIBRARY_ALL_WA
  verifiedWith:
  - test/verify/yosupo-maximum-independent-set.test.cpp
documentation_of: graph/others/maximum-independent-set.hpp
layout: document
redirect_from:
- /library/graph/others/maximum-independent-set.hpp
- /library/graph/others/maximum-independent-set.hpp.html
title: graph/others/maximum-independent-set.hpp
---
