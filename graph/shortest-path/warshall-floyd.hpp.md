---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-grl-1-c.test.cpp
    title: test/verify/aoj-grl-1-c.test.cpp
  _isVerificationFailed: false
  _pathExtension: hpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    document_title: "Warshall Floyd(\u5168\u70B9\u5BFE\u9593\u6700\u77ED\u8DEF)"
    links: []
  bundledCode: "#line 1 \"graph/shortest-path/warshall-floyd.hpp\"\n/**\n * @brief\
    \ Warshall Floyd(\u5168\u70B9\u5BFE\u9593\u6700\u77ED\u8DEF)\n */\ntemplate< typename\
    \ Matrix, typename T >\nvoid warshall_floyd(Matrix &g, T INF) {\n  for(size_t\
    \ k = 0; k < g.size(); k++) {\n    for(size_t i = 0; i < g.size(); i++) {\n  \
    \    for(size_t j = 0; j < g.size(); j++) {\n        if(g[i][k] == INF || g[k][j]\
    \ == INF) continue;\n        g[i][j] = min(g[i][j], g[i][k] + g[k][j]);\n    \
    \  }\n    }\n  }\n}\n"
  code: "/**\n * @brief Warshall Floyd(\u5168\u70B9\u5BFE\u9593\u6700\u77ED\u8DEF\
    )\n */\ntemplate< typename Matrix, typename T >\nvoid warshall_floyd(Matrix &g,\
    \ T INF) {\n  for(size_t k = 0; k < g.size(); k++) {\n    for(size_t i = 0; i\
    \ < g.size(); i++) {\n      for(size_t j = 0; j < g.size(); j++) {\n        if(g[i][k]\
    \ == INF || g[k][j] == INF) continue;\n        g[i][j] = min(g[i][j], g[i][k]\
    \ + g[k][j]);\n      }\n    }\n  }\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/shortest-path/warshall-floyd.hpp
  requiredBy: []
  timestamp: '2021-07-14 01:17:14+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-grl-1-c.test.cpp
documentation_of: graph/shortest-path/warshall-floyd.hpp
layout: document
redirect_from:
- /library/graph/shortest-path/warshall-floyd.hpp
- /library/graph/shortest-path/warshall-floyd.hpp.html
title: "Warshall Floyd(\u5168\u70B9\u5BFE\u9593\u6700\u77ED\u8DEF)"
---
