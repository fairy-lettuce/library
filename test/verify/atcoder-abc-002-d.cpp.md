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
  bundledCode: "#line 1 \"test/verify/atcoder-abc-002-d.cpp\"\n#define IGNORE\n\n\
    int main() {\n  int N, M;\n  cin >> N >> M;\n  Matrix< bool > g(N, vector< bool\
    \ >(N));\n  for(int i = 0; i < M; i++) {\n    int x, y;\n    cin >> x >> y;\n\
    \    --x, --y;\n    g[x][y] = true;\n    g[y][x] = true;\n  }\n  function< int(vector<\
    \ int >) > f = [](vector< int > t) { return t.size(); };\n  cout << maximum_clique(g,\
    \ f) << endl;\n}\n"
  code: "#define IGNORE\n\nint main() {\n  int N, M;\n  cin >> N >> M;\n  Matrix<\
    \ bool > g(N, vector< bool >(N));\n  for(int i = 0; i < M; i++) {\n    int x,\
    \ y;\n    cin >> x >> y;\n    --x, --y;\n    g[x][y] = true;\n    g[y][x] = true;\n\
    \  }\n  function< int(vector< int >) > f = [](vector< int > t) { return t.size();\
    \ };\n  cout << maximum_clique(g, f) << endl;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/atcoder-abc-002-d.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/atcoder-abc-002-d.cpp
layout: document
redirect_from:
- /library/test/verify/atcoder-abc-002-d.cpp
- /library/test/verify/atcoder-abc-002-d.cpp.html
title: test/verify/atcoder-abc-002-d.cpp
---
