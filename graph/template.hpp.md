---
data:
  _extendedDependsOn: []
  _extendedRequiredBy:
  - icon: ':heavy_check_mark:'
    path: graph/others/enumerate-cliques.hpp
    title: "Enumerate-Cliques(\u30AF\u30EA\u30FC\u30AF\u5168\u5217\u6319)"
  - icon: ':heavy_check_mark:'
    path: graph/others/maximum-independent-set.hpp
    title: graph/others/maximum-independent-set.hpp
  - icon: ':heavy_check_mark:'
    path: graph/shortest-path/warshall-floyd.hpp
    title: graph/shortest-path/warshall-floyd.hpp
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-2306.test.cpp
    title: test/verify/aoj-2306.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-grl-1-c.test.cpp
    title: test/verify/aoj-grl-1-c.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-maximum-independent-set.test.cpp
    title: test/verify/yosupo-maximum-independent-set.test.cpp
  _isVerificationFailed: false
  _pathExtension: hpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links: []
  bundledCode: "#line 2 \"graph/template.hpp\"\n\ntemplate< typename T >\nstruct edge\
    \ {\n  int src, to;\n  T cost;\n\n  edge(int to, T cost) : src(-1), to(to), cost(cost)\
    \ {}\n\n  edge(int src, int to, T cost) : src(src), to(to), cost(cost) {}\n\n\
    \  edge &operator=(const int &x) {\n    to = x;\n    return *this;\n  }\n\n  operator\
    \ int() const { return to; }\n};\n\ntemplate< typename T >\nusing Edges = vector<\
    \ edge< T > >;\ntemplate< typename T >\nusing WeightedGraph = vector< Edges< T\
    \ > >;\nusing UnWeightedGraph = vector< vector< int > >;\ntemplate< typename T\
    \ >\nusing Matrix = vector< vector< T > >;\n"
  code: "#pragma once\n\ntemplate< typename T >\nstruct edge {\n  int src, to;\n \
    \ T cost;\n\n  edge(int to, T cost) : src(-1), to(to), cost(cost) {}\n\n  edge(int\
    \ src, int to, T cost) : src(src), to(to), cost(cost) {}\n\n  edge &operator=(const\
    \ int &x) {\n    to = x;\n    return *this;\n  }\n\n  operator int() const { return\
    \ to; }\n};\n\ntemplate< typename T >\nusing Edges = vector< edge< T > >;\ntemplate<\
    \ typename T >\nusing WeightedGraph = vector< Edges< T > >;\nusing UnWeightedGraph\
    \ = vector< vector< int > >;\ntemplate< typename T >\nusing Matrix = vector< vector<\
    \ T > >;\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/template.hpp
  requiredBy:
  - graph/others/enumerate-cliques.hpp
  - graph/others/maximum-independent-set.hpp
  - graph/shortest-path/warshall-floyd.hpp
  timestamp: '2021-07-01 02:53:34+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-grl-1-c.test.cpp
  - test/verify/aoj-2306.test.cpp
  - test/verify/yosupo-maximum-independent-set.test.cpp
documentation_of: graph/template.hpp
layout: document
redirect_from:
- /library/graph/template.hpp
- /library/graph/template.hpp.html
title: graph/template.hpp
---
