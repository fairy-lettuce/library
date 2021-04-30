---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':x:'
    path: test/verify/aoj-grl-1-c.test.cpp
    title: test/verify/aoj-grl-1-c.test.cpp
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes:
    links: []
  bundledCode: "#line 1 \"graph/shortest-path/warshall-floyd.cpp\"\ntemplate< typename\
    \ T >\nvoid warshall_floyd(Matrix< T > &g, T INF) {\n  for(int k = 0; k < g.size();\
    \ k++) {\n    for(int i = 0; i < g.size(); i++) {\n      for(int j = 0; j < g.size();\
    \ j++) {\n        if(g[i][k] == INF || g[k][j] == INF) continue;\n        g[i][j]\
    \ = min(g[i][j], g[i][k] + g[k][j]);\n      }\n    }\n  }\n}\n"
  code: "template< typename T >\nvoid warshall_floyd(Matrix< T > &g, T INF) {\n  for(int\
    \ k = 0; k < g.size(); k++) {\n    for(int i = 0; i < g.size(); i++) {\n     \
    \ for(int j = 0; j < g.size(); j++) {\n        if(g[i][k] == INF || g[k][j] ==\
    \ INF) continue;\n        g[i][j] = min(g[i][j], g[i][k] + g[k][j]);\n      }\n\
    \    }\n  }\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/shortest-path/warshall-floyd.cpp
  requiredBy: []
  timestamp: '2019-11-30 23:02:43+09:00'
  verificationStatus: LIBRARY_ALL_WA
  verifiedWith:
  - test/verify/aoj-grl-1-c.test.cpp
documentation_of: graph/shortest-path/warshall-floyd.cpp
layout: document
redirect_from:
- /library/graph/shortest-path/warshall-floyd.cpp
- /library/graph/shortest-path/warshall-floyd.cpp.html
title: graph/shortest-path/warshall-floyd.cpp
---
