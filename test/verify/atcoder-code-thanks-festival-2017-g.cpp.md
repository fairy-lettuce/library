---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 1 \"test/verify/atcoder-code-thanks-festival-2017-g.cpp\"\n\
    #define IGNORE\n\nint main() {\n  int N, M;\n  cin >> N >> M;\n  Matrix< int >\
    \ g(N, vector< int >(N));\n  for(int i = 0; i < M; i++) {\n    int x, y;\n   \
    \ cin >> x >> y;\n    --x, --y;\n    g[x][y] = g[y][x] = true;\n  }\n  cout <<\
    \ maximum_independent_set(g).size() << endl;\n}\n"
  code: "#define IGNORE\n\nint main() {\n  int N, M;\n  cin >> N >> M;\n  Matrix<\
    \ int > g(N, vector< int >(N));\n  for(int i = 0; i < M; i++) {\n    int x, y;\n\
    \    cin >> x >> y;\n    --x, --y;\n    g[x][y] = g[y][x] = true;\n  }\n  cout\
    \ << maximum_independent_set(g).size() << endl;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/atcoder-code-thanks-festival-2017-g.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/atcoder-code-thanks-festival-2017-g.cpp
layout: document
redirect_from:
- /library/test/verify/atcoder-code-thanks-festival-2017-g.cpp
- /library/test/verify/atcoder-code-thanks-festival-2017-g.cpp.html
title: test/verify/atcoder-code-thanks-festival-2017-g.cpp
---
