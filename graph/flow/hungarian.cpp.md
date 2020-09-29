---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-1163.test.cpp
    title: test/verify/aoj-1163.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links: []
  bundledCode: "#line 1 \"graph/flow/hungarian.cpp\"\ntemplate< typename T >\nT hungarian(Matrix<\
    \ T > &A) {\n  const T infty = numeric_limits< T >::max();\n  const int N = (int)\
    \ A.size();\n  const int M = (int) A[0].size();\n  vector< int > P(M), way(M);\n\
    \  vector< T > U(N, 0), V(M, 0), minV;\n  vector< bool > used;\n\n  for(int i\
    \ = 1; i < N; i++) {\n    P[0] = i;\n    minV.assign(M, infty);\n    used.assign(M,\
    \ false);\n    int j0 = 0;\n    while(P[j0] != 0) {\n      int i0 = P[j0], j1\
    \ = 0;\n      used[j0] = true;\n      T delta = infty;\n      for(int j = 1; j\
    \ < M; j++) {\n        if(used[j]) continue;\n        T curr = A[i0][j] - U[i0]\
    \ - V[j];\n        if(curr < minV[j]) minV[j] = curr, way[j] = j0;\n        if(minV[j]\
    \ < delta) delta = minV[j], j1 = j;\n      }\n      for(int j = 0; j < M; j++)\
    \ {\n        if(used[j]) U[P[j]] += delta, V[j] -= delta;\n        else minV[j]\
    \ -= delta;\n      }\n      j0 = j1;\n    }\n    do {\n      P[j0] = P[way[j0]];\n\
    \      j0 = way[j0];\n    } while(j0 != 0);\n  }\n  return -V[0];\n}\n"
  code: "template< typename T >\nT hungarian(Matrix< T > &A) {\n  const T infty =\
    \ numeric_limits< T >::max();\n  const int N = (int) A.size();\n  const int M\
    \ = (int) A[0].size();\n  vector< int > P(M), way(M);\n  vector< T > U(N, 0),\
    \ V(M, 0), minV;\n  vector< bool > used;\n\n  for(int i = 1; i < N; i++) {\n \
    \   P[0] = i;\n    minV.assign(M, infty);\n    used.assign(M, false);\n    int\
    \ j0 = 0;\n    while(P[j0] != 0) {\n      int i0 = P[j0], j1 = 0;\n      used[j0]\
    \ = true;\n      T delta = infty;\n      for(int j = 1; j < M; j++) {\n      \
    \  if(used[j]) continue;\n        T curr = A[i0][j] - U[i0] - V[j];\n        if(curr\
    \ < minV[j]) minV[j] = curr, way[j] = j0;\n        if(minV[j] < delta) delta =\
    \ minV[j], j1 = j;\n      }\n      for(int j = 0; j < M; j++) {\n        if(used[j])\
    \ U[P[j]] += delta, V[j] -= delta;\n        else minV[j] -= delta;\n      }\n\
    \      j0 = j1;\n    }\n    do {\n      P[j0] = P[way[j0]];\n      j0 = way[j0];\n\
    \    } while(j0 != 0);\n  }\n  return -V[0];\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/flow/hungarian.cpp
  requiredBy: []
  timestamp: '2019-11-30 23:02:43+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-1163.test.cpp
documentation_of: graph/flow/hungarian.cpp
layout: document
redirect_from:
- /library/graph/flow/hungarian.cpp
- /library/graph/flow/hungarian.cpp.html
title: graph/flow/hungarian.cpp
---
