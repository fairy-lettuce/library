---
data:
  _extendedDependsOn:
  - icon: ':question:'
    path: graph/template.hpp
    title: graph/template.hpp
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-grl-1-c.test.cpp
    title: test/verify/aoj-grl-1-c.test.cpp
  _isVerificationFailed: false
  _pathExtension: hpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links: []
  bundledCode: "#line 2 \"graph/shortest-path/warshall-floyd.hpp\"\n\n#line 2 \"graph/template.hpp\"\
    \n\ntemplate< typename T >\nstruct edge {\n  int src, to;\n  T cost;\n\n  edge(int\
    \ to, T cost) : src(-1), to(to), cost(cost) {}\n\n  edge(int src, int to, T cost)\
    \ : src(src), to(to), cost(cost) {}\n\n  edge &operator=(const int &x) {\n   \
    \ to = x;\n    return *this;\n  }\n\n  operator int() const { return to; }\n};\n\
    \ntemplate< typename T >\nusing Edges = vector< edge< T > >;\ntemplate< typename\
    \ T >\nusing WeightedGraph = vector< Edges< T > >;\nusing UnWeightedGraph = vector<\
    \ vector< int > >;\ntemplate< typename T >\nusing Matrix = vector< vector< T >\
    \ >;\n#line 4 \"graph/shortest-path/warshall-floyd.hpp\"\n\ntemplate< typename\
    \ T >\nvoid warshall_floyd(Matrix< T > &g, T INF) {\n  for(size_t k = 0; k < g.size();\
    \ k++) {\n    for(size_t i = 0; i < g.size(); i++) {\n      for(size_t j = 0;\
    \ j < g.size(); j++) {\n        if(g[i][k] == INF || g[k][j] == INF) continue;\n\
    \        g[i][j] = min(g[i][j], g[i][k] + g[k][j]);\n      }\n    }\n  }\n}\n"
  code: "#pragma once\n\n#include \"../template.hpp\"\n\ntemplate< typename T >\n\
    void warshall_floyd(Matrix< T > &g, T INF) {\n  for(size_t k = 0; k < g.size();\
    \ k++) {\n    for(size_t i = 0; i < g.size(); i++) {\n      for(size_t j = 0;\
    \ j < g.size(); j++) {\n        if(g[i][k] == INF || g[k][j] == INF) continue;\n\
    \        g[i][j] = min(g[i][j], g[i][k] + g[k][j]);\n      }\n    }\n  }\n}\n"
  dependsOn:
  - graph/template.hpp
  isVerificationFile: false
  path: graph/shortest-path/warshall-floyd.hpp
  requiredBy: []
  timestamp: '2021-07-01 02:53:34+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-grl-1-c.test.cpp
documentation_of: graph/shortest-path/warshall-floyd.hpp
layout: document
redirect_from:
- /library/graph/shortest-path/warshall-floyd.hpp
- /library/graph/shortest-path/warshall-floyd.hpp.html
title: graph/shortest-path/warshall-floyd.hpp
---
