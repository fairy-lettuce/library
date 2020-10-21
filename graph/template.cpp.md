---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-1163.test.cpp
    title: test/verify/aoj-1163.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-2306.test.cpp
    title: test/verify/aoj-2306.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-grl-1-c.test.cpp
    title: test/verify/aoj-grl-1-c.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-grl-2-b.test.cpp
    title: test/verify/aoj-grl-2-b.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-maximum-independent-set.test.cpp
    title: test/verify/yosupo-maximum-independent-set.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links: []
  bundledCode: "#line 1 \"graph/template.cpp\"\ntemplate< typename T >\nstruct edge\
    \ {\n  int src, to;\n  T cost;\n\n  edge(int to, T cost) : src(-1), to(to), cost(cost)\
    \ {}\n\n  edge(int src, int to, T cost) : src(src), to(to), cost(cost) {}\n\n\
    \  edge &operator=(const int &x) {\n    to = x;\n    return *this;\n  }\n\n  operator\
    \ int() const { return to; }\n};\n\ntemplate< typename T >\nusing Edges = vector<\
    \ edge< T > >;\ntemplate< typename T >\nusing WeightedGraph = vector< Edges< T\
    \ > >;\nusing UnWeightedGraph = vector< vector< int > >;\ntemplate< typename T\
    \ >\nusing Matrix = vector< vector< T > >;\n"
  code: "template< typename T >\nstruct edge {\n  int src, to;\n  T cost;\n\n  edge(int\
    \ to, T cost) : src(-1), to(to), cost(cost) {}\n\n  edge(int src, int to, T cost)\
    \ : src(src), to(to), cost(cost) {}\n\n  edge &operator=(const int &x) {\n   \
    \ to = x;\n    return *this;\n  }\n\n  operator int() const { return to; }\n};\n\
    \ntemplate< typename T >\nusing Edges = vector< edge< T > >;\ntemplate< typename\
    \ T >\nusing WeightedGraph = vector< Edges< T > >;\nusing UnWeightedGraph = vector<\
    \ vector< int > >;\ntemplate< typename T >\nusing Matrix = vector< vector< T >\
    \ >;\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/template.cpp
  requiredBy: []
  timestamp: '2019-07-20 01:29:30+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-2306.test.cpp
  - test/verify/aoj-grl-2-b.test.cpp
  - test/verify/yosupo-maximum-independent-set.test.cpp
  - test/verify/aoj-grl-1-c.test.cpp
  - test/verify/aoj-1163.test.cpp
documentation_of: graph/template.cpp
layout: document
redirect_from:
- /library/graph/template.cpp
- /library/graph/template.cpp.html
title: graph/template.cpp
---
